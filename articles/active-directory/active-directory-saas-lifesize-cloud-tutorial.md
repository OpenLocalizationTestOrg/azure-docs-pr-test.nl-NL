---
title: 'Zelfstudie: Azure Active Directory-integratie met Lifesize Cloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Lifesize Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="1a3fc-103">Zelfstudie: Azure Active Directory-integratie met Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="1a3fc-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="1a3fc-104">In deze zelfstudie leert u hoe Lifesize Cloud integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a3fc-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a3fc-105">Lifesize Cloud integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a3fc-106">U kunt beheren in Azure AD die toegang tot Lifesize Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="1a3fc-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="1a3fc-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Lifesize Cloud (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="1a3fc-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a3fc-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1a3fc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1a3fc-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a3fc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a3fc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a3fc-110">Prerequisites</span></span>

<span data-ttu-id="1a3fc-111">Voor het configureren van Azure AD-integratie met Lifesize Cloud, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="1a3fc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1a3fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a3fc-113">Een Lifesize Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1a3fc-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a3fc-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a3fc-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a3fc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a3fc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a3fc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a3fc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1a3fc-118">Scenario description</span></span>
<span data-ttu-id="1a3fc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a3fc-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a3fc-121">Lifesize Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a3fc-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="1a3fc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a3fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="1a3fc-123">Lifesize Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a3fc-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="1a3fc-124">Voor het configureren van de integratie van Lifesize Cloud met Azure AD, moet u Lifesize Cloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a3fc-125">**Als u wilt toevoegen Lifesize Cloud uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a3fc-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a3fc-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a3fc-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1a3fc-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1a3fc-133">Typ in het zoekvak **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="1a3fc-135">Selecteer in het deelvenster resultaten **Lifesize Cloud**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a3fc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a3fc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a3fc-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Lifesize Cloud op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a3fc-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de Lifesize Cloud is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="1a3fc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Lifesize Cloud tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="1a3fc-141">In de Lifesize Cloud, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a3fc-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Lifesize Cloud, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a3fc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1a3fc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a3fc-145">**[Maken van een testgebruiker Lifesize Cloud](#creating-a-lifesize-cloud-test-user)**  - Lifesize Cloud die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a3fc-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a3fc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a3fc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1a3fc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a3fc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="1a3fc-150">**Om eenmalige aanmelding Azure AD met Lifesize Cloud configureert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1a3fc-151">In de Azure-portal op de **Lifesize Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1a3fc-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="1a3fc-155">Op de **Lifesize Cloud-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="1a3fc-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-157">a.</span></span> <span data-ttu-id="1a3fc-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="1a3fc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="1a3fc-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-159">b.</span></span> <span data-ttu-id="1a3fc-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1a3fc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="1a3fc-161">Controleer **weergeven geavanceerde instellingen voor URL**, voer de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="1a3fc-163">In de **Relay-status** textbox, typ een URL met het volgende patroon volgen:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="1a3fc-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="1a3fc-164">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-164">Please note that these are not the real values.</span></span> <span data-ttu-id="1a3fc-165">u hebt deze waarden bijwerken met de werkelijke aanmeldings-URL, Relay-status en -id.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="1a3fc-166">Neem contact op met [Lifesize Cloud Client ondersteuningsteam](https://www.lifesize.com/support) ophalen aanmeldings-URL, en id-waarden en u kunt benutten Relay status SSO-configuratie die verderop in de zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="1a3fc-167">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="1a3fc-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a3fc-171">Op de **Lifesize Cloudconfiguratie** sectie, klikt u op **Lifesize Cloud configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1a3fc-172">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="1a3fc-174">Ophalen van eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, aanmelding bij de toepassing Lifesize Cloud met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="1a3fc-175">Klik op uw naam in de rechterbovenhoek en klik vervolgens op de **geavanceerde instellingen**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="1a3fc-177">In de geavanceerde instellingen en klik nu op de **SSO configuratie** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="1a3fc-178">De configuratiepagina van eenmalige aanmelding voor uw exemplaar, wordt deze geopend.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="1a3fc-180">Configureer nu de volgende waarden in de configuratie van de SSO-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="1a3fc-182">a.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-182">a.</span></span> <span data-ttu-id="1a3fc-183">In **identiteit Provider verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1a3fc-184">b.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-184">b.</span></span>  <span data-ttu-id="1a3fc-185">In **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1a3fc-186">c.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-186">c.</span></span> <span data-ttu-id="1a3fc-187">De base-64 gecodeerde certificaat openen in Kladblok van Azure portal hebt gedownload, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="1a3fc-188">d.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-188">d.</span></span> <span data-ttu-id="1a3fc-189">Toewijzingen voor het tekstvak Voornaam Voer de waarde als in het SAML-kenmerk **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="1a3fc-190">e.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-190">e.</span></span> <span data-ttu-id="1a3fc-191">In de toewijzing van SAML-kenmerk voor de **achternaam** tekstvak voert u de waarde als **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="1a3fc-192">f.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-192">f.</span></span> <span data-ttu-id="1a3fc-193">In de toewijzing van SAML-kenmerk voor de **e** tekstvak voert u de waarde als **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="1a3fc-194">Controleer de configuratie kunt u op de **Test** knop.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1a3fc-195">Voor het testen van geslaagde moet u de configuratiewizard kunt voltooien in Azure AD en ook toegang te bieden aan gebruikers of groepen die de test kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="1a3fc-196">De eenmalige aanmelding inschakelen door te controleren op de **eenmalige aanmelding inschakelen** knop.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="1a3fc-197">Klik nu op de **Update** knop zodat alle instellingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="1a3fc-198">Hierdoor wordt de waarde RelayState gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-198">This will generate the RelayState value.</span></span> <span data-ttu-id="1a3fc-199">Kopieer de waarde RelayState, die wordt gegenereerd in het tekstvak, plak deze in de **Relay status** textbox onder **Lifesize Cloud-domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="1a3fc-200">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1a3fc-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a3fc-201">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a3fc-202">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a3fc-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a3fc-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1a3fc-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="1a3fc-204">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1a3fc-206">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a3fc-207">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a3fc-209">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a3fc-211">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a3fc-213">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a3fc-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a3fc-215">a.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-215">a.</span></span> <span data-ttu-id="1a3fc-216">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a3fc-217">b.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-217">b.</span></span> <span data-ttu-id="1a3fc-218">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a3fc-219">c.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-219">c.</span></span> <span data-ttu-id="1a3fc-220">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1a3fc-221">d.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-221">d.</span></span> <span data-ttu-id="1a3fc-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="1a3fc-223">Een testgebruiker Lifesize Cloud maken</span><span class="sxs-lookup"><span data-stu-id="1a3fc-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="1a3fc-224">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in de Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="1a3fc-225">Lifesize cloud biedt ondersteuning voor automatisch gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="1a3fc-226">Na de geslaagde verificatie op Azure AD worden de gebruiker automatisch ingericht in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1a3fc-227">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a3fc-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1a3fc-228">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1a3fc-230">**Britta Simon om aan te wijzen Lifesize Cloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a3fc-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1a3fc-231">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1a3fc-233">Selecteer in de lijst met toepassingen **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="1a3fc-235">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1a3fc-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-237">Click **Add** button.</span></span> <span data-ttu-id="1a3fc-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1a3fc-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1a3fc-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a3fc-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a3fc-243">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a3fc-243">Testing single sign-on</span></span>

<span data-ttu-id="1a3fc-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1a3fc-245">Als u op de tegel Lifesize Cloud in het deelvenster toegang, krijgt u de aanmeldingspagina van Lifesize Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a3fc-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="1a3fc-246">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a3fc-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a3fc-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1a3fc-247">Additional resources</span></span>

* [<span data-ttu-id="1a3fc-248">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a3fc-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a3fc-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a3fc-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

