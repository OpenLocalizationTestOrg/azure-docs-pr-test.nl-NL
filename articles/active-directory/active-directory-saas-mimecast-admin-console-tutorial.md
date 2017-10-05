---
title: 'Zelfstudie: Azure Active Directory-integratie met Mimecast-beheerconsole | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Mimecast-beheerconsole.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="31900-103">Zelfstudie: Azure Active Directory-integratie met Mimecast-beheerconsole</span><span class="sxs-lookup"><span data-stu-id="31900-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="31900-104">In deze zelfstudie leert u hoe de beheerconsole Mimecast integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31900-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31900-105">Beheerconsole Mimecast integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="31900-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31900-106">U kunt beheren in Azure AD die toegang tot Mimecast-beheerconsole heeft.</span><span class="sxs-lookup"><span data-stu-id="31900-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="31900-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de beheerconsole Mimecast (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="31900-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="31900-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="31900-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="31900-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31900-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31900-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="31900-110">Prerequisites</span></span>

<span data-ttu-id="31900-111">Voor het configureren van Azure AD-integratie met Mimecast-beheerconsole, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="31900-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="31900-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="31900-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31900-113">Een beheerconsole Mimecast eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="31900-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31900-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="31900-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31900-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="31900-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31900-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="31900-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31900-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31900-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31900-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="31900-118">Scenario description</span></span>
<span data-ttu-id="31900-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="31900-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31900-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="31900-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31900-121">Mimecast-beheerconsole uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="31900-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="31900-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31900-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="31900-123">Mimecast-beheerconsole uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="31900-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="31900-124">Voor het configureren van de integratie van Mimecast-beheerconsole in Azure AD, moet u Mimecast-beheerconsole uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="31900-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31900-125">**Als u wilt toevoegen Mimecast-beheerconsole uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31900-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31900-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="31900-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="31900-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31900-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31900-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31900-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="31900-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31900-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="31900-133">Typ in het zoekvak **Mimecast-beheerconsole**, selecteer **Mimecast-beheerconsole** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="31900-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Mimecast-beheerconsole in de lijst met resultaten](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="31900-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="31900-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="31900-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Mimecast-beheerconsole op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="31900-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31900-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de beheerconsole Mimecast is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31900-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="31900-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de beheerconsole Mimecast tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="31900-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="31900-139">In de beheerconsole Mimecast, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="31900-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31900-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Mimecast-beheerconsole, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="31900-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31900-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="31900-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31900-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31900-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31900-143">**[Maak een testgebruiker beheerconsole Mimecast](#create-a-mimecast-admin-console-test-user)**  - Mimecast-beheerconsole die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="31900-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31900-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="31900-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31900-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="31900-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="31900-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="31900-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="31900-147">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Mimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="31900-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="31900-148">**Voor het configureren van Azure AD eenmalige aanmelding met Mimecast-beheerconsole, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31900-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="31900-149">In de Azure-portal op de **Mimecast-beheerconsole** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="31900-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="31900-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="31900-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="31900-153">Op de **Mimecast Admin Consoledomein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="31900-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Domein Mimecast Administrator-Console en URL's van eenmalige aanmelding informatie](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="31900-155">In de **aanmeldings-URL** textbox, typ de URL:</span><span class="sxs-lookup"><span data-stu-id="31900-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="31900-156">Het teken op de URL voor is specifieke regio.</span><span class="sxs-lookup"><span data-stu-id="31900-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="31900-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="31900-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="31900-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="31900-159">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31900-161">Op de **Mimecast Console beheerdersconfiguratie** sectie, klikt u op **Mimecast beheerconsole configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="31900-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31900-162">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="31900-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuratie van de Console Mimecast Admin](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="31900-164">In een ander browservenster, meld u bij uw Mimecast-beheerconsole als beheerder.</span><span class="sxs-lookup"><span data-stu-id="31900-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="31900-165">Ga naar **Services \> toepassing**.</span><span class="sxs-lookup"><span data-stu-id="31900-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="31900-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span><span class="sxs-lookup"><span data-stu-id="31900-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="31900-167">Klik op **verificatie profielen**.</span><span class="sxs-lookup"><span data-stu-id="31900-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="31900-168">![Verificatie profielen](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "verificatie-profielen")</span><span class="sxs-lookup"><span data-stu-id="31900-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="31900-169">Klik op **nieuwe Authentication profiel**.</span><span class="sxs-lookup"><span data-stu-id="31900-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="31900-170">![Nieuwe verificatie profielen](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "nieuwe verificatie-profielen")</span><span class="sxs-lookup"><span data-stu-id="31900-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="31900-171">In de **Authentication profiel** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="31900-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="31900-172">![Authentication profiel](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication profiel")</span><span class="sxs-lookup"><span data-stu-id="31900-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="31900-173">a.</span><span class="sxs-lookup"><span data-stu-id="31900-173">a.</span></span> <span data-ttu-id="31900-174">In de **beschrijving** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="31900-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="31900-175">b.</span><span class="sxs-lookup"><span data-stu-id="31900-175">b.</span></span> <span data-ttu-id="31900-176">Selecteer **afdwingen van SAML-verificatie voor de beheerconsole Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="31900-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="31900-177">c.</span><span class="sxs-lookup"><span data-stu-id="31900-177">c.</span></span> <span data-ttu-id="31900-178">Als **Provider**, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31900-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="31900-179">d.</span><span class="sxs-lookup"><span data-stu-id="31900-179">d.</span></span> <span data-ttu-id="31900-180">Plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit de Azure-portal in de **URL-verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="31900-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="31900-181">e.</span><span class="sxs-lookup"><span data-stu-id="31900-181">e.</span></span> <span data-ttu-id="31900-182">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit de Azure-portal in de **aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="31900-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="31900-183">f.</span><span class="sxs-lookup"><span data-stu-id="31900-183">f.</span></span> <span data-ttu-id="31900-184">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit de Azure-portal in de **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="31900-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="31900-185">De waarde van de aanmeldings-URL en de afmelding URL-waarde zijn voor de beheerconsole Mimecast hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="31900-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="31900-186">g.</span><span class="sxs-lookup"><span data-stu-id="31900-186">g.</span></span> <span data-ttu-id="31900-187">Open uw base 64-certificaat gedownload vanuit Azure-portal in Kladblok, verwijdert u de eerste regel ('*--*') en de laatste regel ('*--*'), kopieert u de resterende inhoud van dit in uw Klembord en plakt u deze naar de **Provider identiteitscertificaat (metagegevens)** textbox.</span><span class="sxs-lookup"><span data-stu-id="31900-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="31900-188">h.</span><span class="sxs-lookup"><span data-stu-id="31900-188">h.</span></span> <span data-ttu-id="31900-189">Selecteer **toestaan voor eenmalige op**.</span><span class="sxs-lookup"><span data-stu-id="31900-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="31900-190">ik.</span><span class="sxs-lookup"><span data-stu-id="31900-190">i.</span></span> <span data-ttu-id="31900-191">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="31900-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="31900-192">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="31900-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31900-193">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="31900-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31900-194">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31900-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="31900-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="31900-195">Create an Azure AD test user</span></span>

<span data-ttu-id="31900-196">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="31900-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="31900-198">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31900-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31900-199">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="31900-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="31900-201">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="31900-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="31900-203">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31900-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="31900-205">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="31900-205">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="31900-207">a.</span><span class="sxs-lookup"><span data-stu-id="31900-207">a.</span></span> <span data-ttu-id="31900-208">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31900-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31900-209">b.</span><span class="sxs-lookup"><span data-stu-id="31900-209">b.</span></span> <span data-ttu-id="31900-210">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31900-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="31900-211">c.</span><span class="sxs-lookup"><span data-stu-id="31900-211">c.</span></span> <span data-ttu-id="31900-212">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="31900-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="31900-213">d.</span><span class="sxs-lookup"><span data-stu-id="31900-213">d.</span></span> <span data-ttu-id="31900-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="31900-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="31900-215">Maak een testgebruiker Mimecast-beheerconsole</span><span class="sxs-lookup"><span data-stu-id="31900-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="31900-216">Om in te schakelen gebruikers van Azure AD aan te melden bij Mimecast-beheerconsole, moeten ze worden ingericht in Mimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="31900-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="31900-217">Inrichting is een handmatige taak in het geval van Mimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="31900-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="31900-218">U moet een domein registreren voordat u gebruikers kunt maken.</span><span class="sxs-lookup"><span data-stu-id="31900-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="31900-219">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31900-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="31900-220">Meld u aan bij uw **Mimecast-beheerconsole** als administrator.</span><span class="sxs-lookup"><span data-stu-id="31900-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="31900-221">Ga naar **mappen \> interne**.</span><span class="sxs-lookup"><span data-stu-id="31900-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="31900-222">![Mappen](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "mappen")</span><span class="sxs-lookup"><span data-stu-id="31900-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="31900-223">Klik op **nieuwe domein registreren**.</span><span class="sxs-lookup"><span data-stu-id="31900-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="31900-224">![Nieuwe domein registreren](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "nieuwe domein registreren")</span><span class="sxs-lookup"><span data-stu-id="31900-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="31900-225">Nadat het nieuwe domein is gemaakt, klikt u op **nieuw adres**.</span><span class="sxs-lookup"><span data-stu-id="31900-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="31900-226">![Nieuw adres](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "nieuw adres")</span><span class="sxs-lookup"><span data-stu-id="31900-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="31900-227">Voer de volgende stappen uit in het dialoogvenster Nieuw adres:</span><span class="sxs-lookup"><span data-stu-id="31900-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="31900-228">![Sla](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "opslaan")</span><span class="sxs-lookup"><span data-stu-id="31900-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="31900-229">a.</span><span class="sxs-lookup"><span data-stu-id="31900-229">a.</span></span> <span data-ttu-id="31900-230">Typ de **e-mailadres**, **globale naam**, **wachtwoord**, en **wachtwoord bevestigen** kenmerken van een geldige Azure AD-account u wilt in te richten in de bijbehorende tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="31900-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="31900-231">b.</span><span class="sxs-lookup"><span data-stu-id="31900-231">b.</span></span> <span data-ttu-id="31900-232">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="31900-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="31900-233">U kunt geen andere hulpprogramma's voor Mimecast-beheerconsole gebruiker-account maken of API's die worden geleverd door Mimecast-beheerconsole gebruiken voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="31900-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="31900-234">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="31900-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="31900-235">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen aan Mimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="31900-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="31900-237">**Britta Simon om aan te wijzen Mimecast-beheerconsole, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="31900-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="31900-238">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="31900-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="31900-240">Selecteer in de lijst met toepassingen **Mimecast-beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="31900-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![De koppeling Mimecast-beheerconsole in de lijst met toepassingen](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="31900-242">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="31900-242">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="31900-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="31900-244">Click **Add** button.</span></span> <span data-ttu-id="31900-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31900-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="31900-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="31900-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31900-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31900-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31900-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="31900-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="31900-250">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="31900-250">Test single sign-on</span></span>

<span data-ttu-id="31900-251">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="31900-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31900-252">Als u op de tegel Mimecast-beheerconsole in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Mimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="31900-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="31900-253">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31900-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="31900-254">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="31900-254">Additional resources</span></span>

* [<span data-ttu-id="31900-255">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31900-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31900-256">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31900-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

