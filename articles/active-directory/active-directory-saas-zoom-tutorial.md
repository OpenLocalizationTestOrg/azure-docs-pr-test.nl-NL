---
title: 'Zelfstudie: Azure Active Directory-integratie met Inzoomen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory- en uitzoomen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: aab491f162fd4d24c6ff4d8858f2edd96dda30d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="f6b61-103">Zelfstudie: Azure Active Directory-integratie met zoomen</span><span class="sxs-lookup"><span data-stu-id="f6b61-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="f6b61-104">In deze zelfstudie leert u hoe zoomen integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6b61-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6b61-105">Inzoomen integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f6b61-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f6b61-106">U kunt beheren in Azure AD die toegang tot Zoom heeft.</span><span class="sxs-lookup"><span data-stu-id="f6b61-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="f6b61-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Inzoomen (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f6b61-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="f6b61-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f6b61-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6b61-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6b61-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f6b61-110">Prerequisites</span></span>

<span data-ttu-id="f6b61-111">Voor het configureren van Azure AD-integratie met inzoomen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f6b61-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="f6b61-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f6b61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6b61-113">Een zoomen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f6b61-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6b61-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f6b61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6b61-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f6b61-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6b61-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f6b61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6b61-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6b61-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6b61-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f6b61-118">Scenario description</span></span>
<span data-ttu-id="f6b61-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f6b61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6b61-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f6b61-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6b61-121">Inzoomen op uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f6b61-121">Adding Zoom from the gallery</span></span>
2. <span data-ttu-id="f6b61-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6b61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="f6b61-123">Inzoomen op uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f6b61-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="f6b61-124">Voor het configureren van de integratie van zoomen met Azure AD, die u wilt inzoomen op uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f6b61-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f6b61-125">**Als u wilt inzoomen op uit de galerie toevoegen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6b61-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f6b61-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f6b61-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="f6b61-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f6b61-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="f6b61-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b61-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="f6b61-133">Typ in het zoekvak **zoomen**, selecteer **zoomen** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6b61-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![Zoomt u in de lijst met resultaten](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f6b61-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6b61-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f6b61-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Inzoomen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f6b61-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6b61-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in zoomen is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6b61-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="f6b61-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in zoomen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f6b61-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="f6b61-139">Wijs in zoomen, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f6b61-140">Om te configureren en testen van Azure AD eenmalige aanmelding met inzoomen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f6b61-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f6b61-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6b61-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f6b61-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6b61-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6b61-143">**[Maak een testgebruiker zoomen](#create-a-zoom-test-user)**  - zoomen die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f6b61-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6b61-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6b61-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f6b61-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f6b61-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f6b61-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f6b61-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Zoom.</span><span class="sxs-lookup"><span data-stu-id="f6b61-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="f6b61-148">**Voor het configureren van Azure AD eenmalige aanmelding met inzoomen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6b61-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="f6b61-149">In de Azure-portal op de **zoomen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f6b61-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="f6b61-153">Op de **domein zoomen en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f6b61-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Domein- en URL's eenmalige aanmelding informatie zoomen](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="f6b61-155">a.</span><span class="sxs-lookup"><span data-stu-id="f6b61-155">a.</span></span> <span data-ttu-id="f6b61-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="f6b61-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="f6b61-157">b.</span><span class="sxs-lookup"><span data-stu-id="f6b61-157">b.</span></span> <span data-ttu-id="f6b61-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="f6b61-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6b61-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f6b61-159">These values are not real.</span></span> <span data-ttu-id="f6b61-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="f6b61-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f6b61-161">Neem contact op met [Client zoomen ondersteuningsteam](https://support.zoom.us/hc) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f6b61-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span> 
 
4. <span data-ttu-id="f6b61-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f6b61-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="f6b61-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f6b61-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6b61-166">Op de **zoomen configuratie** sectie, klikt u op **configureren zoomen** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f6b61-166">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f6b61-167">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f6b61-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Inzoomen-configuratie](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="f6b61-169">In een ander browservenster, meld u aan bij uw bedrijf zoomen site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f6b61-169">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="f6b61-170">Klik op de **Single Sign-On** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f6b61-170">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="f6b61-171">![Eenmalige aanmelding op het tabblad](./media/active-directory-saas-zoom-tutorial/IC784700.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="f6b61-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="f6b61-172">Klik op de **beveiligingscontrole** tabblad en gaat u naar de **Single Sign-On** instellingen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-172">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="f6b61-173">Voer de volgende stappen uit in de sectie eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="f6b61-173">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="f6b61-174">![Eenmalige aanmelding sectie](./media/active-directory-saas-zoom-tutorial/IC784701.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="f6b61-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="f6b61-175">a.</span><span class="sxs-lookup"><span data-stu-id="f6b61-175">a.</span></span> <span data-ttu-id="f6b61-176">In de **aanmelden pagina-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f6b61-176">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f6b61-177">b.</span><span class="sxs-lookup"><span data-stu-id="f6b61-177">b.</span></span> <span data-ttu-id="f6b61-178">In de **afmelden pagina-URL** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f6b61-178">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="f6b61-179">c.</span><span class="sxs-lookup"><span data-stu-id="f6b61-179">c.</span></span> <span data-ttu-id="f6b61-180">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="f6b61-180">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="f6b61-181">d.</span><span class="sxs-lookup"><span data-stu-id="f6b61-181">d.</span></span> <span data-ttu-id="f6b61-182">In de **verlener** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f6b61-182">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="f6b61-183">e.</span><span class="sxs-lookup"><span data-stu-id="f6b61-183">e.</span></span> <span data-ttu-id="f6b61-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f6b61-185">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f6b61-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f6b61-186">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f6b61-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f6b61-187">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6b61-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f6b61-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f6b61-188">Create an Azure AD test user</span></span>

<span data-ttu-id="f6b61-189">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="f6b61-191">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6b61-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f6b61-192">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="f6b61-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f6b61-194">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f6b61-196">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b61-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f6b61-198">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f6b61-198">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f6b61-200">a.</span><span class="sxs-lookup"><span data-stu-id="f6b61-200">a.</span></span> <span data-ttu-id="f6b61-201">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6b61-202">b.</span><span class="sxs-lookup"><span data-stu-id="f6b61-202">b.</span></span> <span data-ttu-id="f6b61-203">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6b61-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f6b61-204">c.</span><span class="sxs-lookup"><span data-stu-id="f6b61-204">c.</span></span> <span data-ttu-id="f6b61-205">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="f6b61-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f6b61-206">d.</span><span class="sxs-lookup"><span data-stu-id="f6b61-206">d.</span></span> <span data-ttu-id="f6b61-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="f6b61-208">Maak een testgebruiker zoomen</span><span class="sxs-lookup"><span data-stu-id="f6b61-208">Create a Zoom test user</span></span>

<span data-ttu-id="f6b61-209">Om Azure AD-gebruikers zich aanmelden bij zoomen inschakelen, moeten ze ingericht in zoomen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-209">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="f6b61-210">In het geval van Inzoomen is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="f6b61-210">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="f6b61-211">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f6b61-211">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="f6b61-212">Meld u aan bij uw **zoomen** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f6b61-212">Log in to your **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="f6b61-213">Klik op de **accountbeheer** tabblad en klik vervolgens op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-213">Click the **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="f6b61-214">Klik in de sectie beheer van de gebruiker op **gebruikers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-214">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="f6b61-215">![Gebruikersbeheer](./media/active-directory-saas-zoom-tutorial/IC784703.png "Gebruikersbeheer")</span><span class="sxs-lookup"><span data-stu-id="f6b61-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="f6b61-216">Op de **gebruikers toevoegen** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f6b61-216">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="f6b61-217">![Gebruikers toevoegen](./media/active-directory-saas-zoom-tutorial/IC784704.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="f6b61-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="f6b61-218">a.</span><span class="sxs-lookup"><span data-stu-id="f6b61-218">a.</span></span> <span data-ttu-id="f6b61-219">Als **gebruikerstype**, selecteer **Basic**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="f6b61-220">b.</span><span class="sxs-lookup"><span data-stu-id="f6b61-220">b.</span></span> <span data-ttu-id="f6b61-221">In de **e-mailberichten** textbox, typ het e-mailadres van een geldige Azure AD-account u wilt inrichten.</span><span class="sxs-lookup"><span data-stu-id="f6b61-221">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="f6b61-222">c.</span><span class="sxs-lookup"><span data-stu-id="f6b61-222">c.</span></span> <span data-ttu-id="f6b61-223">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="f6b61-224">U kunt andere zoomen gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door inzoomen om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="f6b61-224">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f6b61-225">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="f6b61-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="f6b61-226">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan zoomen.</span><span class="sxs-lookup"><span data-stu-id="f6b61-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="f6b61-228">**Britta Simon om aan te wijzen inzoomen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6b61-228">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="f6b61-229">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f6b61-231">Selecteer in de lijst met toepassingen **zoomen**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-231">In the applications list, select **Zoom**.</span></span>

    ![De koppeling inzoomen in de lijst met toepassingen](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="f6b61-233">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f6b61-233">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="f6b61-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f6b61-235">Click **Add** button.</span></span> <span data-ttu-id="f6b61-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b61-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="f6b61-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f6b61-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f6b61-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b61-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6b61-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b61-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f6b61-241">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6b61-241">Test single sign-on</span></span>

<span data-ttu-id="f6b61-242">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f6b61-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f6b61-243">Als u op de tegel Zoom in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Zoom.</span><span class="sxs-lookup"><span data-stu-id="f6b61-243">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6b61-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f6b61-244">Additional resources</span></span>

* [<span data-ttu-id="f6b61-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6b61-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6b61-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6b61-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

