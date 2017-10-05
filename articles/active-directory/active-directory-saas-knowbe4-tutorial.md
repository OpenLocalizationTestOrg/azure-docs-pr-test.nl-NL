---
title: 'Zelfstudie: Azure Active Directory-integratie met KnowBe4 Awareness beveiligingstraining | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en KnowBe4 Awareness beveiligingstraining.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 3b18737112a8aef101fab7fac1904f7c2e194d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="83e7c-103">Zelfstudie: Azure Active Directory-integratie met KnowBe4 Awareness beveiligingstraining</span><span class="sxs-lookup"><span data-stu-id="83e7c-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="83e7c-104">In deze zelfstudie leert u hoe KnowBe4 Awareness beveiligingstraining integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83e7c-104">In this tutorial, you learn how to integrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83e7c-105">KnowBe4 Awareness beveiligingstraining integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="83e7c-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83e7c-106">U kunt beheren in Azure AD die toegang tot de beveiligingstraining Awareness KnowBe4 heeft</span><span class="sxs-lookup"><span data-stu-id="83e7c-106">You can control in Azure AD who has access to KnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="83e7c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij KnowBe4 beveiligingstraining Awareness (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="83e7c-107">You can enable your users to automatically get signed-on to KnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83e7c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="83e7c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="83e7c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83e7c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83e7c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="83e7c-110">Prerequisites</span></span>

<span data-ttu-id="83e7c-111">Voor het configureren van Azure AD-integratie met KnowBe4 Awareness beveiligingstraining, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="83e7c-111">To configure Azure AD integration with KnowBe4 Security Awareness Training, you need the following items:</span></span>

- <span data-ttu-id="83e7c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="83e7c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83e7c-113">Een KnowBe4 Awareness beveiligingstraining eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="83e7c-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83e7c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="83e7c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83e7c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="83e7c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83e7c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="83e7c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83e7c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83e7c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83e7c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="83e7c-118">Scenario description</span></span>
<span data-ttu-id="83e7c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="83e7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83e7c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="83e7c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83e7c-121">KnowBe4 Awareness beveiligingstraining uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="83e7c-121">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
2. <span data-ttu-id="83e7c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="83e7c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-the-gallery"></a><span data-ttu-id="83e7c-123">KnowBe4 Awareness beveiligingstraining uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="83e7c-123">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
<span data-ttu-id="83e7c-124">Voor het configureren van de integratie van KnowBe4 Awareness beveiligingstraining in Azure AD, moet u KnowBe4 Awareness beveiligingstraining uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="83e7c-124">To configure the integration of KnowBe4 Security Awareness Training into Azure AD, you need to add KnowBe4 Security Awareness Training from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83e7c-125">**Als u wilt toevoegen KnowBe4 Awareness beveiligingstraining uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="83e7c-125">**To add KnowBe4 Security Awareness Training from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83e7c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="83e7c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83e7c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83e7c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="83e7c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83e7c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="83e7c-133">Typ in het zoekvak **KnowBe4 Awareness beveiligingstraining**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-133">In the search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="83e7c-135">Selecteer in het deelvenster resultaten **KnowBe4 Awareness beveiligingstraining**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="83e7c-135">In the results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83e7c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="83e7c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83e7c-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met KnowBe4 Awareness beveiligingstraining op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="83e7c-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83e7c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in KnowBe4 Awareness beveiligingstraining is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83e7c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 Security Awareness Training is to a user in Azure AD.</span></span> <span data-ttu-id="83e7c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in KnowBe4 Awareness beveiligingstraining tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="83e7c-140">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 Security Awareness Training needs to be established.</span></span>

<span data-ttu-id="83e7c-141">Wijs in KnowBe4 Awareness beveiligingstraining, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="83e7c-141">In KnowBe4 Security Awareness Training, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83e7c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met KnowBe4 Awareness beveiligingstraining, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="83e7c-142">To configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83e7c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="83e7c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83e7c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83e7c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83e7c-145">**[Maken van een testgebruiker KnowBe4 Awareness beveiligingstraining](#creating-a-knowbe4-security-awareness-training-test-user)**  - KnowBe4 Awareness beveiligingstraining die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="83e7c-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - to have a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="83e7c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="83e7c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83e7c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="83e7c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83e7c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="83e7c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83e7c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing KnowBe4 Awareness beveiligingstraining configureren.</span><span class="sxs-lookup"><span data-stu-id="83e7c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="83e7c-150">**Voor het configureren van Azure AD eenmalige aanmelding met KnowBe4 Awareness beveiligingstraining, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="83e7c-150">**To configure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="83e7c-151">In de Azure-portal op de **KnowBe4 Awareness beveiligingstraining** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-151">In the Azure portal, on the **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="83e7c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="83e7c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="83e7c-155">Op de **Awareness KnowBe4-Training beveiligingsdomein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="83e7c-155">On the **KnowBe4 Security Awareness Training Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="83e7c-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="83e7c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83e7c-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="83e7c-158">The value is not real.</span></span> <span data-ttu-id="83e7c-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="83e7c-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="83e7c-160">Neem contact op met [KnowBe4 beveiliging Awareness Training Client ondersteuningsteam](mailto:support@KnowBe4.com) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="83e7c-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) to get the value.</span></span> 
 

4. <span data-ttu-id="83e7c-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="83e7c-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="83e7c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="83e7c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="83e7c-165">Op de **Awareness KnowBe4-Training Beveiligingsconfiguratie** sectie, klikt u op **configureren KnowBe4 Awareness beveiligingstraining** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="83e7c-165">On the **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** to open **Configure sign-on** window.</span></span> <span data-ttu-id="83e7c-166">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="83e7c-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="83e7c-168">Eenmalige aanmelding configureren op **KnowBe4 Awareness beveiligingstraining** zijde, moet u de gedownloade verzenden **certificaat (Raw)**, **Sign-Out-URL, SAML entiteit-ID en eenmalige aanmelding SAML Service-URL** naar [KnowBe4 beveiliging Awareness Training Client ondersteuningsteam](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="83e7c-168">To configure single sign-on on **KnowBe4 Security Awareness Training** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="83e7c-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="83e7c-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="83e7c-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="83e7c-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="83e7c-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83e7c-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83e7c-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="83e7c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="83e7c-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="83e7c-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="83e7c-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="83e7c-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83e7c-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="83e7c-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83e7c-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83e7c-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83e7c-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83e7c-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="83e7c-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83e7c-184">a.</span><span class="sxs-lookup"><span data-stu-id="83e7c-184">a.</span></span> <span data-ttu-id="83e7c-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83e7c-186">b.</span><span class="sxs-lookup"><span data-stu-id="83e7c-186">b.</span></span> <span data-ttu-id="83e7c-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83e7c-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83e7c-188">c.</span><span class="sxs-lookup"><span data-stu-id="83e7c-188">c.</span></span> <span data-ttu-id="83e7c-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="83e7c-190">d.</span><span class="sxs-lookup"><span data-stu-id="83e7c-190">d.</span></span> <span data-ttu-id="83e7c-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="83e7c-192">Een testgebruiker KnowBe4 Awareness beveiligingstraining maken</span><span class="sxs-lookup"><span data-stu-id="83e7c-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="83e7c-193">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in KnowBe4 Awareness beveiligingstraining.</span><span class="sxs-lookup"><span data-stu-id="83e7c-193">The objective of this section is to create a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="83e7c-194">KnowBe4 Awareness beveiligingstraining ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="83e7c-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="83e7c-195">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="83e7c-195">There is no action item for you in this section.</span></span> <span data-ttu-id="83e7c-196">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot de beveiligingstraining Awareness KnowBe4 als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="83e7c-196">A new user is created during an attempt to access KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="83e7c-197">Als u een gebruiker handmatig maken wilt, moet u contact op met de [KnowBe4 Awareness beveiligingstraining ondersteuningsteam](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="83e7c-197">If you need to create a user manually, you need to contact the [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="83e7c-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="83e7c-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="83e7c-199">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan KnowBe4 Awareness beveiligingstraining.</span><span class="sxs-lookup"><span data-stu-id="83e7c-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowBe4 Security Awareness Training.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="83e7c-201">**Britta Simon om aan te wijzen KnowBe4 Awareness beveiligingstraining, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="83e7c-201">**To assign Britta Simon to KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="83e7c-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="83e7c-204">Selecteer in de lijst met toepassingen **KnowBe4 Awareness beveiligingstraining**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-204">In the applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="83e7c-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="83e7c-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="83e7c-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="83e7c-208">Click **Add** button.</span></span> <span data-ttu-id="83e7c-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83e7c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="83e7c-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="83e7c-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83e7c-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83e7c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83e7c-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83e7c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83e7c-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="83e7c-214">Testing single sign-on</span></span>

<span data-ttu-id="83e7c-215">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="83e7c-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="83e7c-216">Als u op de tegel KnowBe4 Awareness beveiligingstraining in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing KnowBe4 Awareness beveiligingstraining.</span><span class="sxs-lookup"><span data-stu-id="83e7c-216">When you click the KnowBe4 Security Awareness Training tile in the Access Panel, you should get automatically signed-on to your KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83e7c-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="83e7c-217">Additional resources</span></span>

* [<span data-ttu-id="83e7c-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83e7c-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83e7c-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83e7c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

