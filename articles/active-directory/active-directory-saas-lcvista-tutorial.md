---
title: 'Zelfstudie: Azure Active Directory-integratie met LCVista | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LCVista.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="3f528-103">Zelfstudie: Azure Active Directory-integratie met LCVista</span><span class="sxs-lookup"><span data-stu-id="3f528-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="3f528-104">In deze zelfstudie leert u hoe LCVista integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f528-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f528-105">LCVista integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3f528-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f528-106">U kunt beheren in Azure AD die toegang tot LCVista heeft</span><span class="sxs-lookup"><span data-stu-id="3f528-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="3f528-107">U kunt uw gebruikers automatisch ophalen aangemeld bij LCVista (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3f528-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f528-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3f528-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3f528-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f528-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f528-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f528-110">Prerequisites</span></span>

<span data-ttu-id="3f528-111">Voor het configureren van Azure AD-integratie met LCVista, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3f528-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="3f528-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3f528-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f528-113">Een LCVista eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3f528-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f528-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f528-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f528-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3f528-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f528-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3f528-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f528-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f528-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f528-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3f528-118">Scenario description</span></span>
<span data-ttu-id="3f528-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f528-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f528-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3f528-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f528-121">LCVista uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3f528-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="3f528-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f528-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="3f528-123">LCVista uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3f528-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="3f528-124">Voor het configureren van de integratie van LCVista in Azure AD, moet u LCVista uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3f528-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f528-125">**Als u wilt toevoegen LCVista uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f528-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f528-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3f528-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f528-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f528-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f528-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f528-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3f528-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f528-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3f528-133">Typ in het zoekvak **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="3f528-133">In the search box, type **LCVista**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="3f528-135">Selecteer in het deelvenster resultaten **LCVista**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3f528-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f528-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f528-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f528-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met LCVista op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3f528-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3f528-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LCVista is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f528-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="3f528-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in LCVista tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3f528-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="3f528-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in LCVista.</span><span class="sxs-lookup"><span data-stu-id="3f528-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="3f528-142">Om te configureren en testen van Azure AD eenmalige aanmelding met LCVista, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3f528-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f528-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f528-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f528-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f528-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f528-145">**[Maken van een testgebruiker LCVista](#creating-a-lcvista-test-user)**  - LCVista die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3f528-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f528-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3f528-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f528-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3f528-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f528-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3f528-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f528-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing LCVista configureren.</span><span class="sxs-lookup"><span data-stu-id="3f528-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="3f528-150">**Voor het configureren van Azure AD eenmalige aanmelding met LCVista, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f528-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="3f528-151">In de Azure-portal op de **LCVista** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3f528-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3f528-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3f528-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="3f528-155">Op de **LCVista domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3f528-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="3f528-157">a.</span><span class="sxs-lookup"><span data-stu-id="3f528-157">a.</span></span> <span data-ttu-id="3f528-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="3f528-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="3f528-159">b.</span><span class="sxs-lookup"><span data-stu-id="3f528-159">b.</span></span> <span data-ttu-id="3f528-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="3f528-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="3f528-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="3f528-161">These values are not the real.</span></span> <span data-ttu-id="3f528-162">Deze waarden bijwerken met de werkelijke id en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="3f528-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="3f528-163">Neem contact op met [LCVista Client ondersteuningsteam](https://lcvista.com/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3f528-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="3f528-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3f528-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="3f528-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3f528-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3f528-168">Op de **LCVista configuratie** sectie, klikt u op **configureren LCVista** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3f528-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3f528-169">Kopieer de **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3f528-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="3f528-171">Meld u aan op uw toepassing LCVista als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3f528-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="3f528-172">In de **SAML-Config** sectie, Controleer de **SAML inschakelen aanmelding** en voer de details op zoals vermeld in onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="3f528-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="3f528-174">a.</span><span class="sxs-lookup"><span data-stu-id="3f528-174">a.</span></span> <span data-ttu-id="3f528-175">Plak de **URL-verlener** die u hebt gekopieerd uit Azure AD in de **entiteit-ID** sectie.</span><span class="sxs-lookup"><span data-stu-id="3f528-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="3f528-176">b.</span><span class="sxs-lookup"><span data-stu-id="3f528-176">b.</span></span> <span data-ttu-id="3f528-177">Plak de **Single Sign-On Service-URL** die u hebt gekopieerd uit Azure AD in de **URL** sectie.</span><span class="sxs-lookup"><span data-stu-id="3f528-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="3f528-178">c.</span><span class="sxs-lookup"><span data-stu-id="3f528-178">c.</span></span> <span data-ttu-id="3f528-179">De waarde van metagegevens (XML) die u hebt gedownload vanuit Azure-portal, kopiëren **X509Certificate** en plak deze in de **x509-certificaat** sectie.</span><span class="sxs-lookup"><span data-stu-id="3f528-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="3f528-180">d.</span><span class="sxs-lookup"><span data-stu-id="3f528-180">d.</span></span> <span data-ttu-id="3f528-181">In de **voornaam kenmerk** textbox, plak de waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="3f528-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="3f528-182">e.</span><span class="sxs-lookup"><span data-stu-id="3f528-182">e.</span></span> <span data-ttu-id="3f528-183">In de **laatste naamkenmerk** textbox, plak de waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="3f528-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="3f528-184">f.</span><span class="sxs-lookup"><span data-stu-id="3f528-184">f.</span></span> <span data-ttu-id="3f528-185">In de **e kenmerk** textbox, plak de waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="3f528-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="3f528-186">g.</span><span class="sxs-lookup"><span data-stu-id="3f528-186">g.</span></span> <span data-ttu-id="3f528-187">In de **kenmerk Username** textbox, plak de waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="3f528-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="3f528-188">e.</span><span class="sxs-lookup"><span data-stu-id="3f528-188">e.</span></span> <span data-ttu-id="3f528-189">Klik op **opslaan** de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="3f528-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="3f528-190">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3f528-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3f528-191">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3f528-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3f528-192">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f528-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f528-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3f528-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f528-194">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3f528-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3f528-196">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f528-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f528-197">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3f528-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f528-199">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3f528-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f528-201">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f528-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f528-203">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3f528-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f528-205">a.</span><span class="sxs-lookup"><span data-stu-id="3f528-205">a.</span></span> <span data-ttu-id="3f528-206">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f528-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f528-207">b.</span><span class="sxs-lookup"><span data-stu-id="3f528-207">b.</span></span> <span data-ttu-id="3f528-208">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3f528-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f528-209">c.</span><span class="sxs-lookup"><span data-stu-id="3f528-209">c.</span></span> <span data-ttu-id="3f528-210">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3f528-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3f528-211">d.</span><span class="sxs-lookup"><span data-stu-id="3f528-211">d.</span></span> <span data-ttu-id="3f528-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f528-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="3f528-213">Een testgebruiker LCVista maken</span><span class="sxs-lookup"><span data-stu-id="3f528-213">Creating a LCVista test user</span></span>

<span data-ttu-id="3f528-214">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in LCVista maken.</span><span class="sxs-lookup"><span data-stu-id="3f528-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="3f528-215">U moet contact opnemen met [LCVista Client ondersteuningsteam](https://lcvista.com/contact) de gebruikers in de toepassing LCVista toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3f528-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3f528-216">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f528-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3f528-217">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan LCVista.</span><span class="sxs-lookup"><span data-stu-id="3f528-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3f528-219">**Britta Simon om aan te wijzen LCVista, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f528-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="3f528-220">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f528-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3f528-222">Selecteer in de lijst met toepassingen **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="3f528-222">In the applications list, select **LCVista**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="3f528-224">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3f528-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3f528-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3f528-226">Click **Add** button.</span></span> <span data-ttu-id="3f528-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f528-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3f528-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3f528-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f528-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f528-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f528-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f528-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f528-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f528-232">Testing single sign-on</span></span>

<span data-ttu-id="3f528-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3f528-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="3f528-234">Klik op de tegel LCVista in het deelvenster toegang, wordt u omgeleid naar de organisatie aanmelding op de pagina.</span><span class="sxs-lookup"><span data-stu-id="3f528-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="3f528-235">Na een geslaagde aanmelding u zal worden aangemeld bij uw toepassing LCVista.</span><span class="sxs-lookup"><span data-stu-id="3f528-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="3f528-236">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3f528-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f528-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3f528-237">Additional resources</span></span>

* [<span data-ttu-id="3f528-238">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f528-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f528-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f528-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

