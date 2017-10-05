---
title: 'Zelfstudie: Azure Active Directory-integratie met Optimizely | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Optimizely.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="6e74a-103">Zelfstudie: Azure Active Directory-integratie met Optimizely</span><span class="sxs-lookup"><span data-stu-id="6e74a-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="6e74a-104">In deze zelfstudie leert u hoe Optimizely integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e74a-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e74a-105">Optimizely integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6e74a-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e74a-106">U kunt beheren in Azure AD die toegang tot Optimizely heeft</span><span class="sxs-lookup"><span data-stu-id="6e74a-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="6e74a-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Optimizely (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6e74a-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e74a-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6e74a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6e74a-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e74a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e74a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e74a-110">Prerequisites</span></span>

<span data-ttu-id="6e74a-111">Voor het configureren van Azure AD-integratie met Optimizely, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6e74a-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="6e74a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6e74a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e74a-113">Een Optimizely eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6e74a-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e74a-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e74a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e74a-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6e74a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e74a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6e74a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e74a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e74a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e74a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6e74a-118">Scenario description</span></span>
<span data-ttu-id="6e74a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e74a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e74a-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6e74a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e74a-121">Optimizely uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e74a-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="6e74a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e74a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="6e74a-123">Optimizely uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e74a-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="6e74a-124">Voor het configureren van de integratie van Optimizely in Azure AD, moet u Optimizely uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6e74a-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e74a-125">**Als u wilt toevoegen Optimizely uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e74a-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e74a-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e74a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e74a-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e74a-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6e74a-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e74a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6e74a-133">Typ in het zoekvak **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-133">In the search box, type **Optimizely**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="6e74a-135">Selecteer in het deelvenster resultaten **Optimizely**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e74a-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e74a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e74a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e74a-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Optimizely op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6e74a-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e74a-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Optimizely is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e74a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="6e74a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Optimizely tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6e74a-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="6e74a-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6e74a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="6e74a-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Optimizely, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6e74a-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e74a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6e74a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6e74a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e74a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e74a-145">**[Maken van een testgebruiker Optimizely](#creating-an-optimizely-test-user)**  - Optimizely die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e74a-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e74a-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6e74a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e74a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6e74a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e74a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6e74a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e74a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Optimizely configureren.</span><span class="sxs-lookup"><span data-stu-id="6e74a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="6e74a-150">**Voor het configureren van Azure AD eenmalige aanmelding met Optimizely, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e74a-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="6e74a-151">In de Azure-portal op de **Optimizely** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6e74a-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6e74a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="6e74a-155">Op de **Optimizely domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6e74a-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="6e74a-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e74a-157">a.</span></span> <span data-ttu-id="6e74a-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="6e74a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="6e74a-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e74a-159">b.</span></span> <span data-ttu-id="6e74a-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="6e74a-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e74a-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="6e74a-161">These values are not the real.</span></span> <span data-ttu-id="6e74a-162">U kunt de waarde wordt bijgewerkt met de werkelijke aanmeldings-URL en de id, die verderop in de zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="6e74a-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="6e74a-163">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6e74a-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="6e74a-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6e74a-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e74a-167">Op de **Optimizely configuratie** sectie, klikt u op **configureren Optimizely** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6e74a-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e74a-168">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6e74a-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="6e74a-170">Eenmalige aanmelding configureren op **Optimizely** zijde, neem contact op met uw accountmanager Optimizely en bieden de gedownloade **certificaat (Base64)**, en **SAML Single Sign-On Service-URL**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="6e74a-171">In antwoord op uw e-mailadres biedt Optimizely u de aanmelding op URL (Serviceprovider geïnitieerde SSO) en de id (Service Provider entiteit-ID)-waarden.</span><span class="sxs-lookup"><span data-stu-id="6e74a-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="6e74a-172">a.</span><span class="sxs-lookup"><span data-stu-id="6e74a-172">a.</span></span> <span data-ttu-id="6e74a-173">Kopiëren de **Serviceprovider geïnitieerde eenmalige aanmelding URL** opgegeven door Optimizely en plakken in de **aanmelding op URL** textbox in **Optimizely domein en de URL's** sectie in Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e74a-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="6e74a-174">b.</span><span class="sxs-lookup"><span data-stu-id="6e74a-174">b.</span></span> <span data-ttu-id="6e74a-175">Kopieer de **Service Provider entiteit-ID** opgegeven door Optimizely en plakken in de **id** textbox in **Optimizely domein en de URL's** sectie in Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e74a-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="6e74a-176">In een ander browservenster eenmalige aanmelding voor uw toepassing Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6e74a-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="6e74a-177">Klikt u op dat u de accountnaam in de rechterbovenhoek rechterbovenhoek en vervolgens **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="6e74a-179">Schakel het selectievakje in op het tabblad Account **eenmalige aanmelding inschakelen** onder eenmalige aanmelding in de **overzicht** sectie.</span><span class="sxs-lookup"><span data-stu-id="6e74a-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="6e74a-181">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="6e74a-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="6e74a-182">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6e74a-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e74a-183">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6e74a-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e74a-184">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e74a-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e74a-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6e74a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e74a-186">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6e74a-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6e74a-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e74a-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e74a-189">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e74a-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e74a-191">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e74a-193">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e74a-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e74a-195">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6e74a-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e74a-197">a.</span><span class="sxs-lookup"><span data-stu-id="6e74a-197">a.</span></span> <span data-ttu-id="6e74a-198">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e74a-199">b.</span><span class="sxs-lookup"><span data-stu-id="6e74a-199">b.</span></span> <span data-ttu-id="6e74a-200">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e74a-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="6e74a-201">c.</span><span class="sxs-lookup"><span data-stu-id="6e74a-201">c.</span></span> <span data-ttu-id="6e74a-202">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6e74a-203">d.</span><span class="sxs-lookup"><span data-stu-id="6e74a-203">d.</span></span> <span data-ttu-id="6e74a-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="6e74a-205">Een testgebruiker Optimizely maken</span><span class="sxs-lookup"><span data-stu-id="6e74a-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="6e74a-206">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Optimizely maken.</span><span class="sxs-lookup"><span data-stu-id="6e74a-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="6e74a-207">Selecteer op de startpagina **deelnemers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e74a-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="6e74a-208">Nieuwe medewerker toevoegen aan het project: klik op **nieuwe medewerker**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="6e74a-210">Vul in het e-mailadres en een rol toewijzen.</span><span class="sxs-lookup"><span data-stu-id="6e74a-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="6e74a-211">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-211">Click **Invite**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="6e74a-213">Ze ontvangen een e-uitnodiging.</span><span class="sxs-lookup"><span data-stu-id="6e74a-213">They receive an email invite.</span></span> <span data-ttu-id="6e74a-214">Met behulp van het e-mailadres, hebben ze zich aanmelden bij Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6e74a-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6e74a-215">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e74a-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6e74a-216">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6e74a-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6e74a-218">**Britta Simon om aan te wijzen Optimizely, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e74a-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="6e74a-219">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6e74a-221">Selecteer in de lijst met toepassingen **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-221">In the applications list, select **Optimizely**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="6e74a-223">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6e74a-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6e74a-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6e74a-225">Click **Add** button.</span></span> <span data-ttu-id="6e74a-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e74a-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6e74a-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6e74a-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6e74a-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e74a-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e74a-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e74a-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e74a-231">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e74a-231">Testing single sign-on</span></span>

<span data-ttu-id="6e74a-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6e74a-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6e74a-233">Als u op de tegel Optimizely in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6e74a-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6e74a-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6e74a-234">Additional resources</span></span>

* [<span data-ttu-id="6e74a-235">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e74a-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e74a-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e74a-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

