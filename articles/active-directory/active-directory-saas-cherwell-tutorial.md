---
title: 'Zelfstudie: Azure Active Directory-integratie met Cherwell | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Cherwell.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: jeedes
ms.openlocfilehash: 27fedb9caa1ef27693b2267df285d62aab78bc24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="9048d-103">Zelfstudie: Azure Active Directory-integratie met Cherwell</span><span class="sxs-lookup"><span data-stu-id="9048d-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>

<span data-ttu-id="9048d-104">In deze zelfstudie leert u hoe Cherwell integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9048d-104">In this tutorial, you learn how to integrate Cherwell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9048d-105">Cherwell integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9048d-105">Integrating Cherwell with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9048d-106">U kunt beheren in Azure AD die toegang tot Cherwell heeft</span><span class="sxs-lookup"><span data-stu-id="9048d-106">You can control in Azure AD who has access to Cherwell</span></span>
- <span data-ttu-id="9048d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Cherwell (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9048d-107">You can enable your users to automatically get signed-on to Cherwell (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9048d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9048d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9048d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9048d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9048d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9048d-110">Prerequisites</span></span>

<span data-ttu-id="9048d-111">Voor het configureren van Azure AD-integratie met Cherwell, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9048d-111">To configure Azure AD integration with Cherwell, you need the following items:</span></span>

- <span data-ttu-id="9048d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9048d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9048d-113">Een Cherwell eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9048d-113">A Cherwell single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9048d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9048d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9048d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9048d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9048d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9048d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9048d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9048d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9048d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9048d-118">Scenario description</span></span>
<span data-ttu-id="9048d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9048d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9048d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9048d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9048d-121">Cherwell uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9048d-121">Adding Cherwell from the gallery</span></span>
2. <span data-ttu-id="9048d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9048d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cherwell-from-the-gallery"></a><span data-ttu-id="9048d-123">Cherwell uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9048d-123">Adding Cherwell from the gallery</span></span>
<span data-ttu-id="9048d-124">Voor het configureren van de integratie van Cherwell in Azure AD, moet u Cherwell uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9048d-124">To configure the integration of Cherwell into Azure AD, you need to add Cherwell from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9048d-125">**Als u wilt toevoegen Cherwell uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9048d-125">**To add Cherwell from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9048d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9048d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9048d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9048d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9048d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9048d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9048d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9048d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9048d-133">Typ in het zoekvak **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="9048d-133">In the search box, type **Cherwell**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_search.png)

5. <span data-ttu-id="9048d-135">Selecteer in het deelvenster resultaten **Cherwell**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9048d-135">In the results panel, select **Cherwell**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9048d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9048d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9048d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Cherwell op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9048d-138">In this section, you configure and test Azure AD single sign-on with Cherwell based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9048d-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Cherwell is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9048d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cherwell is to a user in Azure AD.</span></span> <span data-ttu-id="9048d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Cherwell tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9048d-140">In other words, a link relationship between an Azure AD user and the related user in Cherwell needs to be established.</span></span>

<span data-ttu-id="9048d-141">Wijs in Cherwell, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9048d-141">In Cherwell, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9048d-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Cherwell, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9048d-142">To configure and test Azure AD single sign-on with Cherwell, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9048d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9048d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9048d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9048d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9048d-145">**[Maken van een testgebruiker Cherwell](#creating-a-cherwell-test-user)**  - Cherwell die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9048d-145">**[Creating a Cherwell test user](#creating-a-cherwell-test-user)** - to have a counterpart of Britta Simon in Cherwell that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9048d-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9048d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9048d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9048d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9048d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9048d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9048d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Cherwell configureren.</span><span class="sxs-lookup"><span data-stu-id="9048d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cherwell application.</span></span>

<span data-ttu-id="9048d-150">**Voor het configureren van Azure AD eenmalige aanmelding met Cherwell, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9048d-150">**To configure Azure AD single sign-on with Cherwell, perform the following steps:**</span></span>

1. <span data-ttu-id="9048d-151">In de Azure-portal op de **Cherwell** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9048d-151">In the Azure portal, on the **Cherwell** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9048d-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9048d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_samlbase.png)

3. <span data-ttu-id="9048d-155">Op de **Cherwell domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9048d-155">On the **Cherwell Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_url.png)

    <span data-ttu-id="9048d-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.cherwellondemand.com/cherwellclient`</span><span class="sxs-lookup"><span data-stu-id="9048d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.cherwellondemand.com/cherwellclient`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9048d-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="9048d-158">This value is not real.</span></span> <span data-ttu-id="9048d-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9048d-159">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="9048d-160">Neem contact op met [Cherwell ondersteuningsteam](https://csm.cherwell.com/contact) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="9048d-160">Contact [Cherwell support team](https://csm.cherwell.com/contact) to get this value.</span></span>
 
4. <span data-ttu-id="9048d-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9048d-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_certificate.png) 

5. <span data-ttu-id="9048d-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9048d-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cherwell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9048d-165">Op de **Cherwell configuratie** sectie, klikt u op **configureren Cherwell** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="9048d-165">On the **Cherwell Configuration** section, click **Configure Cherwell** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9048d-166">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="9048d-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_configure.png) 

7. <span data-ttu-id="9048d-168">Eenmalige aanmelding configureren op **Cherwell** zijde, moet u de gedownloade verzenden **certificaat (Base64)**, **SAML Single Sign-On Service-URL**, en **SAML Entiteit-ID** naar [Cherwell ondersteuningsteam](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="9048d-168">To configure single sign-on on **Cherwell** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Cherwell support team](https://csm.cherwell.com/contact).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="9048d-169">Het ondersteuningsteam Cherwell heeft te maken van de werkelijke SSO-configuratie.</span><span class="sxs-lookup"><span data-stu-id="9048d-169">Your Cherwell support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="9048d-170">U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="9048d-170">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    
> [!TIP]
> <span data-ttu-id="9048d-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9048d-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9048d-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9048d-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9048d-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9048d-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9048d-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9048d-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="9048d-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9048d-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9048d-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9048d-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9048d-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9048d-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cherwell-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9048d-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9048d-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cherwell-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9048d-182">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9048d-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cherwell-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9048d-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9048d-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cherwell-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9048d-186">a.</span><span class="sxs-lookup"><span data-stu-id="9048d-186">a.</span></span> <span data-ttu-id="9048d-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9048d-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9048d-188">b.</span><span class="sxs-lookup"><span data-stu-id="9048d-188">b.</span></span> <span data-ttu-id="9048d-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9048d-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9048d-190">c.</span><span class="sxs-lookup"><span data-stu-id="9048d-190">c.</span></span> <span data-ttu-id="9048d-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9048d-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9048d-192">d.</span><span class="sxs-lookup"><span data-stu-id="9048d-192">d.</span></span> <span data-ttu-id="9048d-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9048d-193">Click **Create**.</span></span>
 
### <a name="creating-a-cherwell-test-user"></a><span data-ttu-id="9048d-194">Een testgebruiker Cherwell maken</span><span class="sxs-lookup"><span data-stu-id="9048d-194">Creating a Cherwell test user</span></span>

<span data-ttu-id="9048d-195">Om Azure AD-gebruikers zich aanmelden bij Cherwell, moeten ze worden ingericht in Cherwell.</span><span class="sxs-lookup"><span data-stu-id="9048d-195">To enable Azure AD users to log in to Cherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="9048d-196">In het geval van Cherwell, de gebruikersaccounts moeten worden gemaakt door uw [Cherwell ondersteuningsteam](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="9048d-196">In the case of Cherwell, the user accounts need to be created by your [Cherwell support team](https://csm.cherwell.com/contact).</span></span>

>[!NOTE]
><span data-ttu-id="9048d-197">U kunt andere Cherwell gebruiker account hulpmiddelen voor het maken of API's geleverd door Cherwell om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="9048d-197">You can use any other Cherwell user account creation tools or APIs provided by Cherwell to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9048d-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="9048d-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9048d-199">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Cherwell.</span><span class="sxs-lookup"><span data-stu-id="9048d-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cherwell.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9048d-201">**Britta Simon om aan te wijzen Cherwell, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9048d-201">**To assign Britta Simon to Cherwell, perform the following steps:**</span></span>

1. <span data-ttu-id="9048d-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9048d-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9048d-204">Selecteer in de lijst met toepassingen **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="9048d-204">In the applications list, select **Cherwell**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_app.png) 

3. <span data-ttu-id="9048d-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9048d-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9048d-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9048d-208">Click **Add** button.</span></span> <span data-ttu-id="9048d-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9048d-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9048d-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9048d-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9048d-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9048d-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9048d-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9048d-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9048d-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9048d-214">Testing single sign-on</span></span>

<span data-ttu-id="9048d-215">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="9048d-215">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="9048d-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9048d-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9048d-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9048d-217">Additional resources</span></span>

* [<span data-ttu-id="9048d-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9048d-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9048d-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9048d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_203.png

