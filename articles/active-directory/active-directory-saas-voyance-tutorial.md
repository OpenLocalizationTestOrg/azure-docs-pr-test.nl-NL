---
title: 'Zelfstudie: Azure Active Directory-integratie met Voyance | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Voyance.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="0b02b-103">Zelfstudie: Azure Active Directory-integratie met Voyance</span><span class="sxs-lookup"><span data-stu-id="0b02b-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="0b02b-104">In deze zelfstudie leert u hoe Voyance integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b02b-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b02b-105">Voyance integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0b02b-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b02b-106">U kunt beheren in Azure AD die toegang tot Voyance heeft</span><span class="sxs-lookup"><span data-stu-id="0b02b-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="0b02b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Voyance (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0b02b-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b02b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0b02b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b02b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b02b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b02b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0b02b-110">Prerequisites</span></span>

<span data-ttu-id="0b02b-111">Voor het configureren van Azure AD-integratie met Voyance, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="0b02b-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="0b02b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0b02b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b02b-113">Een Voyance eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0b02b-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b02b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0b02b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b02b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0b02b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b02b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0b02b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b02b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b02b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b02b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0b02b-118">Scenario description</span></span>
<span data-ttu-id="0b02b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0b02b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b02b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0b02b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b02b-121">Voyance uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0b02b-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="0b02b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b02b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="0b02b-123">Voyance uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0b02b-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="0b02b-124">Voor het configureren van de integratie van Voyance in Azure AD, moet u Voyance uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0b02b-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b02b-125">**Als u wilt toevoegen Voyance uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b02b-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b02b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0b02b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="0b02b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b02b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="0b02b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b02b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="0b02b-133">Typ in het zoekvak **Voyance**, selecteer **Voyance** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b02b-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance in de lijst met resultaten](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0b02b-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b02b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0b02b-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Voyance op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0b02b-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b02b-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Voyance is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b02b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="0b02b-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Voyance tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="0b02b-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="0b02b-139">Wijs in Voyance, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="0b02b-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b02b-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Voyance, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="0b02b-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b02b-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0b02b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b02b-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b02b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b02b-143">**[Maak een testgebruiker Voyance](#create-a-voyance-test-user)**  - Voyance die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="0b02b-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b02b-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0b02b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b02b-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0b02b-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0b02b-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0b02b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0b02b-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Voyance configureren.</span><span class="sxs-lookup"><span data-stu-id="0b02b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="0b02b-148">**Voor het configureren van Azure AD eenmalige aanmelding met Voyance, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b02b-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="0b02b-149">In de Azure-portal op de **Voyance** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0b02b-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0b02b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="0b02b-153">Op de **Voyance domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="0b02b-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Voyance domein en URL's eenmalige aanmelding-informatie voor IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="0b02b-155">a.</span><span class="sxs-lookup"><span data-stu-id="0b02b-155">a.</span></span> <span data-ttu-id="0b02b-156">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="0b02b-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="0b02b-157">b.</span><span class="sxs-lookup"><span data-stu-id="0b02b-157">b.</span></span> <span data-ttu-id="0b02b-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="0b02b-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="0b02b-159">Controleer **weergeven geavanceerde instellingen voor URL** en voer de volgende stap als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="0b02b-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Voyance domein en URL's eenmalige aanmelding-informatie voor SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="0b02b-161">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="0b02b-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0b02b-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="0b02b-162">These values are not real.</span></span> <span data-ttu-id="0b02b-163">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="0b02b-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0b02b-164">Neem contact op met [Voyance Client ondersteuningsteam](mailto:support@nyansa.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="0b02b-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="0b02b-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0b02b-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="0b02b-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0b02b-167">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0b02b-169">Op de **Voyance configuratie** sectie, klikt u op **configureren Voyance** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0b02b-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b02b-170">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0b02b-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Voyance configuratie](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="0b02b-172">In een ander browservenster aanmelding bij uw tenant Voyance als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0b02b-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="0b02b-173">Ga naar de rechterbovenhoek van de navigatiebalk en klik op de vervolgkeuzelijst met de tekst "**Top universiteit**'.</span><span class="sxs-lookup"><span data-stu-id="0b02b-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde Top universiteit configureren](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="0b02b-175">Klik op '**beheerdersinstellingen**'.</span><span class="sxs-lookup"><span data-stu-id="0b02b-175">Click "**Admin Settings**".</span></span>

    ![Eenmalige aanmelding op App aan clientzijde beheerdersinstellingen configureren](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="0b02b-177">Klik op '**gebruikerstoegang**' tabblad.</span><span class="sxs-lookup"><span data-stu-id="0b02b-177">Click "**User Access**" tab.</span></span>

    ![Eenmalige aanmelding configureren voor toegang voor App-zijde van gebruiker](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="0b02b-179">Klik op de '**SSO is uitgeschakeld**' om de Azure AD configureren als een IdP SAML 2.0 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0b02b-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configureren van eenmalige aanmelding op App aan clientzijde SSO is uitgeschakeld knop](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="0b02b-181">Ga naar **SAML v2** sectie en Voer onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0b02b-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Eenmalige aanmelding configureren op App aan clientzijde SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="0b02b-183">a.</span><span class="sxs-lookup"><span data-stu-id="0b02b-183">a.</span></span> <span data-ttu-id="0b02b-184">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="0b02b-185">b.</span><span class="sxs-lookup"><span data-stu-id="0b02b-185">b.</span></span> <span data-ttu-id="0b02b-186">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit de Azure-portal in de **IdP aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0b02b-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="0b02b-187">c.</span><span class="sxs-lookup"><span data-stu-id="0b02b-187">c.</span></span> <span data-ttu-id="0b02b-188">Open uw gedownloade Base64-gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **IdP Cert** textbox.</span><span class="sxs-lookup"><span data-stu-id="0b02b-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="0b02b-189">d.</span><span class="sxs-lookup"><span data-stu-id="0b02b-189">d.</span></span> <span data-ttu-id="0b02b-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0b02b-191">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="0b02b-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b02b-192">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="0b02b-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b02b-193">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b02b-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0b02b-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0b02b-194">Create an Azure AD test user</span></span>

<span data-ttu-id="0b02b-195">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0b02b-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="0b02b-197">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b02b-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b02b-198">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0b02b-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b02b-200">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b02b-202">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b02b-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b02b-204">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0b02b-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b02b-206">a.</span><span class="sxs-lookup"><span data-stu-id="0b02b-206">a.</span></span> <span data-ttu-id="0b02b-207">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b02b-208">b.</span><span class="sxs-lookup"><span data-stu-id="0b02b-208">b.</span></span> <span data-ttu-id="0b02b-209">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0b02b-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b02b-210">c.</span><span class="sxs-lookup"><span data-stu-id="0b02b-210">c.</span></span> <span data-ttu-id="0b02b-211">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b02b-212">d.</span><span class="sxs-lookup"><span data-stu-id="0b02b-212">d.</span></span> <span data-ttu-id="0b02b-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="0b02b-214">Een testgebruiker Voyance maken</span><span class="sxs-lookup"><span data-stu-id="0b02b-214">Create a Voyance test user</span></span>

<span data-ttu-id="0b02b-215">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Voyance genoemd.</span><span class="sxs-lookup"><span data-stu-id="0b02b-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="0b02b-216">Voyance ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0b02b-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="0b02b-217">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="0b02b-217">There is no action item for you in this section.</span></span> <span data-ttu-id="0b02b-218">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot Voyance als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="0b02b-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="0b02b-219">Als u een gebruiker handmatig maken wilt, moet u contact op met [Voyance ondersteuningsteam](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="0b02b-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0b02b-220">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="0b02b-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="0b02b-221">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Voyance.</span><span class="sxs-lookup"><span data-stu-id="0b02b-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Toewijzen van de gebruikersrol][200]

<span data-ttu-id="0b02b-223">**Britta Simon om aan te wijzen Voyance, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b02b-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="0b02b-224">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0b02b-226">Selecteer in de lijst met toepassingen **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-226">In the applications list, select **Voyance**.</span></span>

    ![De koppeling Voyance in de lijst met toepassingen](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="0b02b-228">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0b02b-228">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="0b02b-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0b02b-230">Click **Add** button.</span></span> <span data-ttu-id="0b02b-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b02b-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="0b02b-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0b02b-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b02b-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b02b-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b02b-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b02b-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0b02b-236">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b02b-236">Test single sign-on</span></span>

<span data-ttu-id="0b02b-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0b02b-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0b02b-238">Als u op de tegel Voyance in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Voyance.</span><span class="sxs-lookup"><span data-stu-id="0b02b-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b02b-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0b02b-239">Additional resources</span></span>

* [<span data-ttu-id="0b02b-240">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b02b-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b02b-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b02b-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

