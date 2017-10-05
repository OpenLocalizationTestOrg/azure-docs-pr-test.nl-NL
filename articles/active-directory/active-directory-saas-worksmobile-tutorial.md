---
title: 'Zelfstudie: Azure Active Directory-integratie met WORKS MOBILE | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en werkt MOBILE.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="8c0a9-103">Zelfstudie: Azure Active Directory-integratie met WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="8c0a9-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="8c0a9-104">In deze zelfstudie leert u hoe werkt MOBILE integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c0a9-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c0a9-105">WERKT MOBILE integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8c0a9-106">U kunt beheren in Azure AD die toegang tot WORKS MOBILE heeft</span><span class="sxs-lookup"><span data-stu-id="8c0a9-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="8c0a9-107">U kunt uw gebruikers automatisch ophalen aangemeld bij WORKS MOBILE (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="8c0a9-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c0a9-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8c0a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8c0a9-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c0a9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c0a9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8c0a9-110">Prerequisites</span></span>

<span data-ttu-id="8c0a9-111">Voor het configureren van Azure AD-integratie met MOBILE werkt, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="8c0a9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8c0a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c0a9-113">Een mobiele werkt eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8c0a9-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c0a9-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c0a9-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c0a9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c0a9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c0a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c0a9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8c0a9-118">Scenario description</span></span>
<span data-ttu-id="8c0a9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c0a9-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c0a9-121">WERKT MOBILE uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8c0a9-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="8c0a9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8c0a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="8c0a9-123">WERKT MOBILE uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8c0a9-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="8c0a9-124">Voor het configureren van de integratie van MOBILE werkt in Azure AD, moet u WORKS MOBILE uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8c0a9-125">**Als u wilt toevoegen werkt MOBILE uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8c0a9-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c0a9-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8c0a9-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8c0a9-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8c0a9-133">Typ in het zoekvak **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="8c0a9-135">Selecteer in het deelvenster resultaten **WORKS MOBILE**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c0a9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8c0a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8c0a9-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met WORKS MOBILE op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8c0a9-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8c0a9-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in WORKS MOBILE is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="8c0a9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in WORKS MOBILE tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="8c0a9-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in MOBILE werkt.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="8c0a9-142">Om te configureren en testen van Azure AD eenmalige aanmelding met MOBILE werkt, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8c0a9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8c0a9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c0a9-145">**[Maken van een gebruiker van de test werkt MOBILE](#creating-a-works-mobile-test-user)**  - MOBILE werkt die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c0a9-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c0a9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c0a9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8c0a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c0a9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing werkt MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="8c0a9-150">**Voor het configureren van Azure AD eenmalige aanmelding met MOBILE werkt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="8c0a9-151">In de Azure-portal op de **WORKS MOBILE** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8c0a9-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="8c0a9-155">Op de **WORKS MOBILE domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="8c0a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-157">a.</span></span> <span data-ttu-id="8c0a9-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="8c0a9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="8c0a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-159">b.</span></span> <span data-ttu-id="8c0a9-160">In de **id** textbox, typ de waarde als`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="8c0a9-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8c0a9-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-161">This value is not real.</span></span> <span data-ttu-id="8c0a9-162">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8c0a9-163">Neem contact op met [MOBILE-Client werkt ondersteuningsteam](mailto:dl_ssoinfo@worksmobile.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="8c0a9-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="8c0a9-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8c0a9-168">Op de **configuratie van de mobiele WORKS** sectie, klikt u op **configureren WORKS MOBILE** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8c0a9-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="8c0a9-171">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [WORKS MOBILE ondersteuningsteam](mailto:dl_ssoinfo@worksmobile.com) en geeft u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="8c0a9-172">• De gedownloade **certificaatbestand**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="8c0a9-173">• De **URL voor SAML-Service voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="8c0a9-174">• De **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="8c0a9-175">• De **afmelden URL**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="8c0a9-176">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="8c0a9-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8c0a9-177">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8c0a9-178">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c0a9-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c0a9-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8c0a9-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="8c0a9-180">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8c0a9-182">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8c0a9-183">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c0a9-185">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c0a9-187">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c0a9-189">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8c0a9-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c0a9-191">a.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-191">a.</span></span> <span data-ttu-id="8c0a9-192">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c0a9-193">b.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-193">b.</span></span> <span data-ttu-id="8c0a9-194">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c0a9-195">c.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-195">c.</span></span> <span data-ttu-id="8c0a9-196">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8c0a9-197">d.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-197">d.</span></span> <span data-ttu-id="8c0a9-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="8c0a9-199">Maken van een gebruiker van de test werkt MOBILE</span><span class="sxs-lookup"><span data-stu-id="8c0a9-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="8c0a9-200">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in WORKS MOBILE maken.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="8c0a9-201">Neem contact op met [WORKS MOBILE ondersteuningsteam](mailto:dl_ssoinfo@worksmobile.com) om toe te voegen de gebruikers van het platform werkt MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8c0a9-202">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c0a9-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8c0a9-203">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding werkt mobiele toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8c0a9-205">**Als u wilt toewijzen Britta Simon Mobile werkt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8c0a9-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="8c0a9-206">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8c0a9-208">Selecteer in de lijst met toepassingen **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="8c0a9-210">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8c0a9-212">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-212">Click **Add** button.</span></span> <span data-ttu-id="8c0a9-213">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8c0a9-215">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8c0a9-216">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c0a9-217">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c0a9-218">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8c0a9-218">Testing single sign-on</span></span>

<span data-ttu-id="8c0a9-219">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8c0a9-220">Als u op de tegel MOBILE werkt in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing werkt MOBILE.</span><span class="sxs-lookup"><span data-stu-id="8c0a9-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="8c0a9-221">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8c0a9-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8c0a9-222">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8c0a9-222">Additional resources</span></span>

* [<span data-ttu-id="8c0a9-223">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c0a9-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c0a9-224">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8c0a9-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

