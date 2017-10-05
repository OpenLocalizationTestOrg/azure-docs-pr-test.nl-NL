---
title: 'Zelfstudie: Azure Active Directory-integratie met TOPdesk - openbare | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TOPdesk - openbaar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="bfc70-103">Zelfstudie: Azure Active Directory-integratie met TOPdesk - openbare</span><span class="sxs-lookup"><span data-stu-id="bfc70-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="bfc70-104">In deze zelfstudie leert u hoe integreren TOPdesk - openbare met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfc70-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfc70-105">Integratie van TOPdesk - openbare met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bfc70-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bfc70-106">U kunt beheren in Azure AD die toegang tot TOPdesk - openbaar heeft.</span><span class="sxs-lookup"><span data-stu-id="bfc70-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="bfc70-107">U kunt uw gebruikers automatisch ophalen aangemeld bij TOPdesk - openbare (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bfc70-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bfc70-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="bfc70-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="bfc70-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfc70-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfc70-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bfc70-110">Prerequisites</span></span>

<span data-ttu-id="bfc70-111">Configureren van Azure AD-integratie met TOPdesk - openbaar is, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="bfc70-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="bfc70-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bfc70-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfc70-113">Een TOPdesk - openbare eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bfc70-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfc70-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bfc70-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfc70-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bfc70-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfc70-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bfc70-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfc70-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfc70-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfc70-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bfc70-118">Scenario description</span></span>
<span data-ttu-id="bfc70-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bfc70-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfc70-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bfc70-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfc70-121">TOPdesk - openbare uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bfc70-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="bfc70-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bfc70-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="bfc70-123">TOPdesk - openbare uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bfc70-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="bfc70-124">Om de integratie van TOPdesk - openbare met Azure AD te configureren die u wilt toevoegen TOPdesk - openbare uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bfc70-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bfc70-125">**Als u wilt toevoegen, TOPdesk - openbare uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bfc70-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc70-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bfc70-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="bfc70-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bfc70-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="bfc70-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bfc70-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="bfc70-133">Typ in het zoekvak **TOPdesk - openbare**, selecteer **TOPdesk - openbare** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="bfc70-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk - publiek in de lijst met resultaten](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bfc70-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfc70-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bfc70-136">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met TOPdesk - openbare op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="bfc70-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bfc70-137">Azure AD moet weten wat de equivalente gebruiker in TOPdesk - openbaar is aan een gebruiker in Azure AD voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="bfc70-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="bfc70-138">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in TOPdesk - openbare moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="bfc70-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="bfc70-139">In TOPdesk - openbaar, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="bfc70-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bfc70-140">Configureren en testen Azure AD eenmalige aanmelding met TOPdesk - openbaar is, moet u de volgende bouwstenen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bfc70-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bfc70-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfc70-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bfc70-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfc70-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfc70-143">**[Maken van een TOPdesk - openbare testgebruiker](#create-a-topdesk---public-test-user)**  - TOPdesk - openbare die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="bfc70-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfc70-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bfc70-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfc70-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bfc70-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bfc70-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bfc70-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bfc70-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw TOPdesk - openbare toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="bfc70-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="bfc70-148">**Eenmalige aanmelding Azure AD configureren met TOPdesk - openbaar, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="bfc70-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc70-149">In de Azure-portal op de **TOPdesk - openbare** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bfc70-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bfc70-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="bfc70-153">Op de **TOPdesk - URL's en openbare domein** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bfc70-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![TOPdesk - URL's en openbare domein eenmalige aanmelding informatie](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="bfc70-155">a.</span><span class="sxs-lookup"><span data-stu-id="bfc70-155">a.</span></span> <span data-ttu-id="bfc70-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="bfc70-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="bfc70-157">b.</span><span class="sxs-lookup"><span data-stu-id="bfc70-157">b.</span></span> <span data-ttu-id="bfc70-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="bfc70-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="bfc70-159">c.</span><span class="sxs-lookup"><span data-stu-id="bfc70-159">c.</span></span> <span data-ttu-id="bfc70-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="bfc70-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bfc70-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="bfc70-161">These values are not real.</span></span> <span data-ttu-id="bfc70-162">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="bfc70-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="bfc70-163">Antwoord-URL is explaned verderop in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="bfc70-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="bfc70-164">Neem contact op met [TOPdesk - ondersteuningsteam openbare Client](https://help.topdesk.com/saas/enterprise/user/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="bfc70-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="bfc70-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bfc70-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="bfc70-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bfc70-167">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="bfc70-169">Op de **TOPdesk - configuratie van openbare** sectie, klikt u op **configureren TOPdesk - openbare** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bfc70-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bfc70-170">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bfc70-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TOPdesk - openbare configuratie](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="bfc70-172">Meld u aan bij uw **TOPdesk - openbare** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bfc70-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="bfc70-173">In de **TOPdesk** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="bfc70-174">![Instellingen](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="bfc70-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="bfc70-175">Klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="bfc70-176">![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "aanmeldingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="bfc70-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="bfc70-177">Vouw de **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="bfc70-178">![Algemene](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "algemeen")</span><span class="sxs-lookup"><span data-stu-id="bfc70-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="bfc70-179">In de **openbare** sectie van de **SAML aanmelding** configuratie sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bfc70-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="bfc70-180">![Instellingen voor technische](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "technische instellingen")</span><span class="sxs-lookup"><span data-stu-id="bfc70-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="bfc70-181">a.</span><span class="sxs-lookup"><span data-stu-id="bfc70-181">a.</span></span> <span data-ttu-id="bfc70-182">Klik op **downloaden** downloaden van het metagegevensbestand van de openbare en lokaal opslaan op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bfc70-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="bfc70-183">b.</span><span class="sxs-lookup"><span data-stu-id="bfc70-183">b.</span></span> <span data-ttu-id="bfc70-184">Open het metagegevensbestand van de gedownloade en ga vervolgens naar de **AssertionConsumerService** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bfc70-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="bfc70-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="bfc70-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="bfc70-186">c.</span><span class="sxs-lookup"><span data-stu-id="bfc70-186">c.</span></span> <span data-ttu-id="bfc70-187">Kopieer de **AssertionConsumerService** waarde, plakt u deze waarde in de **antwoord-URL** textbox in **TOPdesk - URL's en openbare domein** sectie.</span><span class="sxs-lookup"><span data-stu-id="bfc70-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="bfc70-188">Voer de volgende stappen uit voor het maken van een certificaatbestand:</span><span class="sxs-lookup"><span data-stu-id="bfc70-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="bfc70-189">![Certificaat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "certificaat")</span><span class="sxs-lookup"><span data-stu-id="bfc70-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="bfc70-190">a.</span><span class="sxs-lookup"><span data-stu-id="bfc70-190">a.</span></span> <span data-ttu-id="bfc70-191">Open het metagegevensbestand gedownloade vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bfc70-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="bfc70-192">b.</span><span class="sxs-lookup"><span data-stu-id="bfc70-192">b.</span></span> <span data-ttu-id="bfc70-193">Vouw de **RoleDescriptor** knooppunt met een **xsi: type** van **ingevoerd: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="bfc70-194">c.</span><span class="sxs-lookup"><span data-stu-id="bfc70-194">c.</span></span> <span data-ttu-id="bfc70-195">Kopieer de waarde van de **X509Certificate** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bfc70-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="bfc70-196">d.</span><span class="sxs-lookup"><span data-stu-id="bfc70-196">d.</span></span> <span data-ttu-id="bfc70-197">Opslaan van de gekopieerde **X509Certificate** waarde lokaal op uw computer in een bestand.</span><span class="sxs-lookup"><span data-stu-id="bfc70-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="bfc70-198">In de **openbare** sectie, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="bfc70-199">![SAML-aanmelding](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML-aanmelding")</span><span class="sxs-lookup"><span data-stu-id="bfc70-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="bfc70-200">Op de **SAML-configuratie-assistent** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bfc70-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="bfc70-201">![SAML-configuratie-assistent](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "assistent voor SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="bfc70-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="bfc70-202">a.</span><span class="sxs-lookup"><span data-stu-id="bfc70-202">a.</span></span> <span data-ttu-id="bfc70-203">Voor het uploaden van uw gedownloade metagegevensbestand vanuit Azure-portal onder **Federatiemetagegevens**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="bfc70-204">b.</span><span class="sxs-lookup"><span data-stu-id="bfc70-204">b.</span></span> <span data-ttu-id="bfc70-205">Voor het uploaden van het certificaatbestand onder **certificaat (RSA)**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="bfc70-206">c.</span><span class="sxs-lookup"><span data-stu-id="bfc70-206">c.</span></span> <span data-ttu-id="bfc70-207">Het logobestand dat u het ondersteuningsteam TOPdesk onder gekregen te uploaden **Logo pictogram**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="bfc70-208">d.</span><span class="sxs-lookup"><span data-stu-id="bfc70-208">d.</span></span> <span data-ttu-id="bfc70-209">In de **naam gebruikerskenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="bfc70-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="bfc70-210">e.</span><span class="sxs-lookup"><span data-stu-id="bfc70-210">e.</span></span> <span data-ttu-id="bfc70-211">In de **weergavenaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="bfc70-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="bfc70-212">f.</span><span class="sxs-lookup"><span data-stu-id="bfc70-212">f.</span></span> <span data-ttu-id="bfc70-213">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bfc70-214">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="bfc70-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bfc70-215">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="bfc70-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bfc70-216">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfc70-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bfc70-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bfc70-217">Create an Azure AD test user</span></span>

<span data-ttu-id="bfc70-218">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bfc70-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="bfc70-220">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bfc70-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc70-221">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="bfc70-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bfc70-223">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bfc70-225">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bfc70-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bfc70-227">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bfc70-227">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bfc70-229">a.</span><span class="sxs-lookup"><span data-stu-id="bfc70-229">a.</span></span> <span data-ttu-id="bfc70-230">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfc70-231">b.</span><span class="sxs-lookup"><span data-stu-id="bfc70-231">b.</span></span> <span data-ttu-id="bfc70-232">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfc70-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="bfc70-233">c.</span><span class="sxs-lookup"><span data-stu-id="bfc70-233">c.</span></span> <span data-ttu-id="bfc70-234">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="bfc70-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="bfc70-235">d.</span><span class="sxs-lookup"><span data-stu-id="bfc70-235">d.</span></span> <span data-ttu-id="bfc70-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="bfc70-237">Een TOPdesk - openbare testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bfc70-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="bfc70-238">Om in te schakelen van Azure AD-gebruikers aan te melden bij TOPdesk - openbaar, ze in TOPdesk - openbare moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="bfc70-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="bfc70-239">In het geval van TOPdesk - openbare inrichting is een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bfc70-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="bfc70-240">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bfc70-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="bfc70-241">Meld u aan bij uw **TOPdesk - openbare** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="bfc70-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="bfc70-242">Klik in het menu bovenaan op **TOPdesk \> nieuw \> ondersteuningsbestanden \> persoon**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="bfc70-243">![Persoon](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "persoon")</span><span class="sxs-lookup"><span data-stu-id="bfc70-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="bfc70-244">In het dialoogvenster nieuwe persoon, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bfc70-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="bfc70-245">![Nieuwe persoon](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "nieuwe persoon")</span><span class="sxs-lookup"><span data-stu-id="bfc70-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="bfc70-246">a.</span><span class="sxs-lookup"><span data-stu-id="bfc70-246">a.</span></span> <span data-ttu-id="bfc70-247">Klik op het tabblad Algemeen.</span><span class="sxs-lookup"><span data-stu-id="bfc70-247">Click the General tab.</span></span>

    <span data-ttu-id="bfc70-248">b.</span><span class="sxs-lookup"><span data-stu-id="bfc70-248">b.</span></span> <span data-ttu-id="bfc70-249">In de **achternaam** textbox, typ de achternaam van de gebruiker zoals Simon</span><span class="sxs-lookup"><span data-stu-id="bfc70-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="bfc70-250">c.</span><span class="sxs-lookup"><span data-stu-id="bfc70-250">c.</span></span> <span data-ttu-id="bfc70-251">Selecteer een **Site** voor het account.</span><span class="sxs-lookup"><span data-stu-id="bfc70-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="bfc70-252">d.</span><span class="sxs-lookup"><span data-stu-id="bfc70-252">d.</span></span> <span data-ttu-id="bfc70-253">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="bfc70-254">U kunt andere TOPdesk - hulpmiddelen voor het maken van account openbaar gebruiker of API's die is geleverd door TOPdesk - openbare voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bfc70-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bfc70-255">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="bfc70-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="bfc70-256">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan TOPdesk - openbare.</span><span class="sxs-lookup"><span data-stu-id="bfc70-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="bfc70-258">**Britta Simon toewijzen aan TOPdesk - openbaar, voer de volgende stappen uit:**</span><span class="sxs-lookup"><span data-stu-id="bfc70-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="bfc70-259">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bfc70-261">Selecteer in de lijst met toepassingen **TOPdesk - openbare**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![De TOPdesk - openbare koppeling in de lijst met toepassingen](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="bfc70-263">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bfc70-263">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="bfc70-265">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bfc70-265">Click **Add** button.</span></span> <span data-ttu-id="bfc70-266">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bfc70-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="bfc70-268">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="bfc70-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bfc70-269">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bfc70-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfc70-270">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bfc70-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bfc70-271">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bfc70-271">Test single sign-on</span></span>

<span data-ttu-id="bfc70-272">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bfc70-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bfc70-273">Wanneer u klikt op de TOPdesk - openbare-tegel in het toegangsvenster, u moet ophalen automatisch aangemeld bij uw TOPdesk - openbare toepassing.</span><span class="sxs-lookup"><span data-stu-id="bfc70-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="bfc70-274">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bfc70-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bfc70-275">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bfc70-275">Additional resources</span></span>

* [<span data-ttu-id="bfc70-276">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfc70-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfc70-277">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfc70-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

