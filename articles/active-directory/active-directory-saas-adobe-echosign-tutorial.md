---
title: 'Zelfstudie: Azure Active Directory-integratie met Adobe teken | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Adobe aanmelding.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="96739-103">Zelfstudie: Azure Active Directory-integratie met Adobe teken</span><span class="sxs-lookup"><span data-stu-id="96739-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="96739-104">In deze zelfstudie leert u hoe Adobe aanmelding integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96739-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96739-105">Meld u Adobe integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="96739-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="96739-106">U kunt beheren in Azure AD die toegang tot Adobe aanmelding heeft</span><span class="sxs-lookup"><span data-stu-id="96739-106">You can control in Azure AD who has access to Adobe Sign</span></span>
- <span data-ttu-id="96739-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Adobe aanmelding (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="96739-107">You can enable your users to automatically get signed-on to Adobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96739-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="96739-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="96739-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96739-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96739-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="96739-110">Prerequisites</span></span>

<span data-ttu-id="96739-111">Voor het configureren van Azure AD-integratie met Adobe teken, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="96739-111">To configure Azure AD integration with Adobe Sign, you need the following items:</span></span>

- <span data-ttu-id="96739-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="96739-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96739-113">Een Adobe aanmelding eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="96739-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96739-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="96739-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96739-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="96739-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96739-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="96739-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96739-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96739-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96739-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="96739-118">Scenario description</span></span>
<span data-ttu-id="96739-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="96739-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96739-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="96739-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96739-121">Adobe teken uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="96739-121">Adding Adobe Sign from the gallery</span></span>
2. <span data-ttu-id="96739-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="96739-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-the-gallery"></a><span data-ttu-id="96739-123">Adobe teken uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="96739-123">Adding Adobe Sign from the gallery</span></span>
<span data-ttu-id="96739-124">Voor het configureren van de integratie van Adobe aanmelding in Azure AD, moet u Adobe teken uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="96739-124">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="96739-125">**Als u wilt toevoegen Adobe teken uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96739-125">**To add Adobe Sign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="96739-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="96739-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96739-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="96739-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="96739-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="96739-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="96739-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96739-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="96739-133">Typ in het zoekvak **Adobe aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="96739-133">In the search box, type **Adobe Sign**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="96739-135">Selecteer in het deelvenster resultaten **Adobe aanmelding**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="96739-135">In the results panel, select **Adobe Sign**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96739-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="96739-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96739-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Adobe aanmelding op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="96739-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="96739-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Adobe aanmelding is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96739-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Sign is to a user in Azure AD.</span></span> <span data-ttu-id="96739-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Adobe aanmelding tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="96739-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Sign needs to be established.</span></span>

<span data-ttu-id="96739-141">Wijs in Adobe teken, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="96739-141">In Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="96739-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Adobe teken, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="96739-142">To configure and test Azure AD single sign-on with Adobe Sign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="96739-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96739-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="96739-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96739-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96739-145">**[Maken van een testgebruiker Adobe aanmelding](#creating-an-adobe-sign-test-user)**  - Adobe-aanmelding die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="96739-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - to have a counterpart of Britta Simon in Adobe Sign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="96739-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="96739-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96739-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="96739-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96739-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="96739-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96739-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Adobe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="96739-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="96739-150">**Voor het configureren van Azure AD eenmalige aanmelding met Adobe teken, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96739-150">**To configure Azure AD single sign-on with Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="96739-151">In de Azure-portal op de **Adobe aanmelding** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="96739-151">In the Azure portal, on the **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="96739-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="96739-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="96739-155">Op de **Adobe aanmelding domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="96739-155">On the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="96739-157">a.</span><span class="sxs-lookup"><span data-stu-id="96739-157">a.</span></span> <span data-ttu-id="96739-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="96739-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="96739-159">b.</span><span class="sxs-lookup"><span data-stu-id="96739-159">b.</span></span> <span data-ttu-id="96739-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="96739-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96739-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="96739-161">These values are not real.</span></span> <span data-ttu-id="96739-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="96739-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="96739-163">Neem contact op met [Adobe aanmelding Client ondersteuningsteam](https://helpx.adobe.com/in/contact/support.html) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="96739-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="96739-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="96739-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="96739-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="96739-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96739-168">Op de **Adobe aanmelding configuratie** sectie, klikt u op **Adobe aanmelding configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="96739-168">On the **Adobe Sign Configuration** section, click **Configure Adobe Sign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="96739-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="96739-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="96739-171">In een ander browservenster, meld u aan bij uw bedrijf Adobe aanmelding site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="96739-171">In a different web browser window, log in to your Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="96739-172">Klik in het menu bovenaan op **Account**, en klik vervolgens in het navigatievenster aan de linkerkant op **SAML instellingen** onder **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="96739-172">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="96739-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span><span class="sxs-lookup"><span data-stu-id="96739-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="96739-174">Voer de volgende stappen uit in de sectie SAML-instellingen:</span><span class="sxs-lookup"><span data-stu-id="96739-174">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="96739-175">![Instellingen voor SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="96739-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="96739-176">a.</span><span class="sxs-lookup"><span data-stu-id="96739-176">a.</span></span> <span data-ttu-id="96739-177">Als **SAML modus**, selecteer **SAML verplichte**.</span><span class="sxs-lookup"><span data-stu-id="96739-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="96739-178">b.</span><span class="sxs-lookup"><span data-stu-id="96739-178">b.</span></span> <span data-ttu-id="96739-179">Selecteer **EchoSign-accountbeheerders toestaan om aan te melden met hun referenties EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="96739-179">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="96739-180">c.</span><span class="sxs-lookup"><span data-stu-id="96739-180">c.</span></span> <span data-ttu-id="96739-181">Als **maken van een gebruikersaccount**, selecteer **automatisch toevoegen van gebruikers worden geverifieerd via SAML**.</span><span class="sxs-lookup"><span data-stu-id="96739-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="96739-182">Verplaatsen op de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="96739-182">Move on, performing the following steps:</span></span>

       <span data-ttu-id="96739-183">![Instellingen voor SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="96739-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="96739-184">a.</span><span class="sxs-lookup"><span data-stu-id="96739-184">a.</span></span> <span data-ttu-id="96739-185">Plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal in de **IdP entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="96739-185">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="96739-186">b.</span><span class="sxs-lookup"><span data-stu-id="96739-186">b.</span></span> <span data-ttu-id="96739-187">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal in de **IdP aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="96739-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="96739-188">c.</span><span class="sxs-lookup"><span data-stu-id="96739-188">c.</span></span> <span data-ttu-id="96739-189">Plakken **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal in de **IdP afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="96739-189">Paste **Sign-Out URL**, which you have copied from Azure portal into the **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="96739-190">d.</span><span class="sxs-lookup"><span data-stu-id="96739-190">d.</span></span> <span data-ttu-id="96739-191">Open uw gedownloade **Certificate(Base64)** bestand in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **IdP certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="96739-191">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>

    <span data-ttu-id="96739-192">e.</span><span class="sxs-lookup"><span data-stu-id="96739-192">e.</span></span> <span data-ttu-id="96739-193">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="96739-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="96739-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="96739-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="96739-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="96739-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="96739-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96739-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96739-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="96739-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="96739-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="96739-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="96739-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96739-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="96739-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="96739-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96739-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="96739-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96739-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96739-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96739-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="96739-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96739-209">a.</span><span class="sxs-lookup"><span data-stu-id="96739-209">a.</span></span> <span data-ttu-id="96739-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96739-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96739-211">b.</span><span class="sxs-lookup"><span data-stu-id="96739-211">b.</span></span> <span data-ttu-id="96739-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96739-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96739-213">c.</span><span class="sxs-lookup"><span data-stu-id="96739-213">c.</span></span> <span data-ttu-id="96739-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="96739-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="96739-215">d.</span><span class="sxs-lookup"><span data-stu-id="96739-215">d.</span></span> <span data-ttu-id="96739-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="96739-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="96739-217">Een testgebruiker Adobe aanmelding maken</span><span class="sxs-lookup"><span data-stu-id="96739-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="96739-218">Om Azure AD-gebruikers zich aanmelden bij Adobe aanmelding, moeten ze worden ingericht in Adobe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="96739-218">To enable Azure AD users to log in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="96739-219">In het geval van Adobe teken is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="96739-219">In the case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="96739-220">U kunt andere Adobe aanmelding gebruiker account hulpmiddelen voor het maken of API's geleverd door Adobe aanmelding aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="96739-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision AAD user accounts.</span></span> 

<span data-ttu-id="96739-221">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96739-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="96739-222">Meld u aan bij uw **Adobe aanmelding** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="96739-222">Log in to your **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="96739-223">Klik in het menu bovenaan op **Account**, en klik vervolgens in het navigatievenster aan de linkerkant op **gebruikers en groepen**, en klik vervolgens op **Maak een nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="96739-223">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="96739-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span><span class="sxs-lookup"><span data-stu-id="96739-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="96739-225">In de **nieuwe gebruiker maken** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="96739-225">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="96739-226">![Gebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="96739-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="96739-227">a.</span><span class="sxs-lookup"><span data-stu-id="96739-227">a.</span></span> <span data-ttu-id="96739-228">Typ de **e-mailadres**, **voornaam**, en **achternaam** van een geldige AAD-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="96739-228">Type the **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="96739-229">b.</span><span class="sxs-lookup"><span data-stu-id="96739-229">b.</span></span> <span data-ttu-id="96739-230">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="96739-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="96739-231">De houder van Azure Active Directory-account ontvangt een e-mailbericht een koppeling om te bevestigen van het account bevat voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="96739-231">The Azure Active Directory account holder receives an email that includes a link to confirm the account before it becomes active.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="96739-232">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="96739-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="96739-233">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen voor het ondertekenen van Adobe.</span><span class="sxs-lookup"><span data-stu-id="96739-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Sign.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="96739-235">**Als u wilt toewijzen Britta Simon Adobe ondertekenen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96739-235">**To assign Britta Simon to Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="96739-236">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="96739-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="96739-238">Selecteer in de lijst met toepassingen **Adobe aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="96739-238">In the applications list, select **Adobe Sign**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="96739-240">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="96739-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="96739-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="96739-242">Click **Add** button.</span></span> <span data-ttu-id="96739-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96739-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="96739-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="96739-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="96739-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96739-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96739-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96739-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96739-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="96739-248">Testing single sign-on</span></span>

<span data-ttu-id="96739-249">Als u op de tegel Adobe teken in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Adobe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="96739-249">When you click the Adobe Sign tile in the Access Panel, you should get automatically signed-on to your Adobe Sign application.</span></span>
<span data-ttu-id="96739-250">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="96739-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96739-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="96739-251">Additional resources</span></span>

* [<span data-ttu-id="96739-252">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96739-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96739-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96739-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

