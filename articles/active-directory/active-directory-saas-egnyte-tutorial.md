---
title: 'Zelfstudie: Azure Active Directory-integratie met Egnyte | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Egnyte.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="5c296-103">Zelfstudie: Azure Active Directory-integratie met Egnyte</span><span class="sxs-lookup"><span data-stu-id="5c296-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="5c296-104">In deze zelfstudie leert u hoe Egnyte integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c296-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c296-105">Egnyte integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5c296-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c296-106">U kunt beheren in Azure AD die toegang tot Egnyte heeft</span><span class="sxs-lookup"><span data-stu-id="5c296-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="5c296-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Egnyte (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="5c296-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c296-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5c296-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c296-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c296-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c296-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5c296-110">Prerequisites</span></span>

<span data-ttu-id="5c296-111">Voor het configureren van Azure AD-integratie met Egnyte, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="5c296-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="5c296-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5c296-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c296-113">Een Egnyte eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5c296-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c296-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5c296-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c296-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5c296-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c296-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5c296-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c296-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c296-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c296-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5c296-118">Scenario description</span></span>
<span data-ttu-id="5c296-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5c296-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c296-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5c296-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c296-121">Egnyte uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5c296-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="5c296-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5c296-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="5c296-123">Egnyte uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5c296-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="5c296-124">Voor het configureren van de integratie van Egnyte in Azure AD, moet u Egnyte uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="5c296-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c296-125">**Als u wilt toevoegen Egnyte uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5c296-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c296-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5c296-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c296-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5c296-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c296-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5c296-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="5c296-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c296-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="5c296-133">Typ in het zoekvak **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="5c296-133">In the search box, type **Egnyte**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="5c296-135">Selecteer in het deelvenster resultaten **Egnyte**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5c296-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c296-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5c296-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c296-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Egnyte op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="5c296-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c296-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Egnyte is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c296-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="5c296-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Egnyte tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="5c296-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="5c296-141">Wijs in Egnyte, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="5c296-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c296-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Egnyte, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="5c296-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c296-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5c296-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c296-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c296-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c296-145">**[Maken van een testgebruiker Egnyte](#creating-an-egnyte-test-user)**  - Egnyte die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="5c296-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c296-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5c296-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c296-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5c296-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c296-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5c296-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c296-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Egnyte configureren.</span><span class="sxs-lookup"><span data-stu-id="5c296-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="5c296-150">**Voor het configureren van Azure AD eenmalige aanmelding met Egnyte, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5c296-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="5c296-151">In de Azure-portal op de **Egnyte** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5c296-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5c296-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5c296-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="5c296-155">Op de **Egnyte domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5c296-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="5c296-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="5c296-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c296-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="5c296-158">This value is not real.</span></span> <span data-ttu-id="5c296-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5c296-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="5c296-160">Neem contact op met [Egnyte Client ondersteuningsteam](https://www.egnyte.com/corp/contact_egnyte.html) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="5c296-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="5c296-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5c296-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="5c296-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5c296-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c296-165">Op de **Egnyte configuratie** sectie, klikt u op **configureren Egnyte** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="5c296-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5c296-166">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="5c296-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="5c296-168">In een ander browservenster, meld u aan bij uw bedrijf Egnyte site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="5c296-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="5c296-169">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5c296-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="5c296-170">![Instellingen](./media/active-directory-saas-egnyte-tutorial/ic787819.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="5c296-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="5c296-171">Klik in het menu **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5c296-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="5c296-172">![Instellingen](./media/active-directory-saas-egnyte-tutorial/ic787820.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="5c296-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="5c296-173">Klik op de **configuratie** tabblad en klik vervolgens op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="5c296-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="5c296-174">![Beveiliging](./media/active-directory-saas-egnyte-tutorial/ic787821.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="5c296-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="5c296-175">In de **eenmalige aanmelding verificatie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5c296-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="5c296-176">![Eenmalige verificatie](./media/active-directory-saas-egnyte-tutorial/ic787822.png "eenmalige-verificatie")</span><span class="sxs-lookup"><span data-stu-id="5c296-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="5c296-177">a.</span><span class="sxs-lookup"><span data-stu-id="5c296-177">a.</span></span> <span data-ttu-id="5c296-178">Als **eenmalige aanmelding verificatie**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5c296-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="5c296-179">b.</span><span class="sxs-lookup"><span data-stu-id="5c296-179">b.</span></span> <span data-ttu-id="5c296-180">Als **identiteitsprovider**, selecteer **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="5c296-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="5c296-181">c.</span><span class="sxs-lookup"><span data-stu-id="5c296-181">c.</span></span> <span data-ttu-id="5c296-182">Plakken **SAML Single Sign-On Service-URL** gekopieerd vanuit Azure-portal in de **identiteit provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="5c296-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="5c296-183">d.</span><span class="sxs-lookup"><span data-stu-id="5c296-183">d.</span></span> <span data-ttu-id="5c296-184">Plakken **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal in de **identiteit provider entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="5c296-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="5c296-185">e.</span><span class="sxs-lookup"><span data-stu-id="5c296-185">e.</span></span> <span data-ttu-id="5c296-186">De base-64 gecodeerde certificaat openen in Kladblok van Azure portal hebt gedownload, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="5c296-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="5c296-187">f.</span><span class="sxs-lookup"><span data-stu-id="5c296-187">f.</span></span> <span data-ttu-id="5c296-188">Als **standaard Gebruikerskoppeling**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="5c296-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="5c296-189">g.</span><span class="sxs-lookup"><span data-stu-id="5c296-189">g.</span></span> <span data-ttu-id="5c296-190">Als **domeinspecifieke verlener waarde**, selecteer **uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="5c296-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="5c296-191">h.</span><span class="sxs-lookup"><span data-stu-id="5c296-191">h.</span></span> <span data-ttu-id="5c296-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5c296-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5c296-193">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="5c296-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c296-194">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="5c296-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c296-195">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c296-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c296-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5c296-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c296-197">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5c296-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="5c296-199">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5c296-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c296-200">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5c296-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c296-202">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5c296-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c296-204">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c296-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c296-206">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5c296-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c296-208">a.</span><span class="sxs-lookup"><span data-stu-id="5c296-208">a.</span></span> <span data-ttu-id="5c296-209">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c296-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c296-210">b.</span><span class="sxs-lookup"><span data-stu-id="5c296-210">b.</span></span> <span data-ttu-id="5c296-211">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c296-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c296-212">c.</span><span class="sxs-lookup"><span data-stu-id="5c296-212">c.</span></span> <span data-ttu-id="5c296-213">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="5c296-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c296-214">d.</span><span class="sxs-lookup"><span data-stu-id="5c296-214">d.</span></span> <span data-ttu-id="5c296-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c296-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="5c296-216">Een testgebruiker Egnyte maken</span><span class="sxs-lookup"><span data-stu-id="5c296-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="5c296-217">Om Azure AD-gebruikers zich aanmelden bij Egnyte, moeten ze worden ingericht in Egnyte.</span><span class="sxs-lookup"><span data-stu-id="5c296-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="5c296-218">In het geval van Egnyte is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="5c296-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="5c296-219">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5c296-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="5c296-220">Meld u aan bij uw **Egnyte** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="5c296-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="5c296-221">Ga naar **instellingen \> gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5c296-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="5c296-222">Klik op **nieuwe gebruiker toevoegen**, en selecteer vervolgens het type van de gebruiker die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5c296-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="5c296-223">![Gebruikers](./media/active-directory-saas-egnyte-tutorial/ic787824.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="5c296-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="5c296-224">In de **nieuwe standaardgebruiker** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5c296-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="5c296-225">![Nieuwe standaardgebruiker](./media/active-directory-saas-egnyte-tutorial/ic787825.png "nieuwe standaardgebruiker")</span><span class="sxs-lookup"><span data-stu-id="5c296-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="5c296-226">a.</span><span class="sxs-lookup"><span data-stu-id="5c296-226">a.</span></span> <span data-ttu-id="5c296-227">Typ de **e**, **gebruikersnaam**, en andere details van een geldig Azure Active Directory-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="5c296-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="5c296-228">b.</span><span class="sxs-lookup"><span data-stu-id="5c296-228">b.</span></span> <span data-ttu-id="5c296-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5c296-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="5c296-230">De houder van Azure Active Directory-account ontvangt een melding per e-mail.</span><span class="sxs-lookup"><span data-stu-id="5c296-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="5c296-231">U kunt andere Egnyte gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Egnyte aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="5c296-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c296-232">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c296-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c296-233">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Egnyte.</span><span class="sxs-lookup"><span data-stu-id="5c296-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="5c296-235">**Britta Simon om aan te wijzen Egnyte, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5c296-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="5c296-236">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5c296-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5c296-238">Selecteer in de lijst met toepassingen **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="5c296-238">In the applications list, select **Egnyte**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="5c296-240">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5c296-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="5c296-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5c296-242">Click **Add** button.</span></span> <span data-ttu-id="5c296-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c296-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="5c296-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5c296-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c296-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c296-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c296-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5c296-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c296-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5c296-248">Testing single sign-on</span></span>

<span data-ttu-id="5c296-249">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="5c296-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c296-250">Als u op de tegel Egnyte in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Egnyte.</span><span class="sxs-lookup"><span data-stu-id="5c296-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="5c296-251">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c296-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5c296-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5c296-252">Additional resources</span></span>

* [<span data-ttu-id="5c296-253">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c296-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c296-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c296-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

