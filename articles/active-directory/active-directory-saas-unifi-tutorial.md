---
title: 'Zelfstudie: Azure Active Directory-integratie met UNIFI | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en UNIFI.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 09074d4628825909f0bb961c8001e53fb06cf7c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="97b41-103">Zelfstudie: Azure Active Directory-integratie met UNIFI</span><span class="sxs-lookup"><span data-stu-id="97b41-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="97b41-104">In deze zelfstudie leert u hoe UNIFI integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97b41-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97b41-105">UNIFI integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="97b41-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="97b41-106">U kunt beheren in Azure AD die toegang tot UNIFI heeft</span><span class="sxs-lookup"><span data-stu-id="97b41-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="97b41-107">U kunt uw gebruikers automatisch ophalen aangemeld bij UNIFI (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="97b41-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97b41-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="97b41-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="97b41-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97b41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97b41-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97b41-110">Prerequisites</span></span>

<span data-ttu-id="97b41-111">Voor het configureren van Azure AD-integratie met UNIFI, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="97b41-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="97b41-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="97b41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97b41-113">Een UNIFI eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="97b41-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97b41-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="97b41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97b41-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="97b41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97b41-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="97b41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97b41-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97b41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97b41-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="97b41-118">Scenario description</span></span>
<span data-ttu-id="97b41-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="97b41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97b41-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="97b41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97b41-121">UNIFI uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="97b41-121">Adding UNIFI from the gallery</span></span>
2. <span data-ttu-id="97b41-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97b41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="97b41-123">UNIFI uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="97b41-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="97b41-124">Voor het configureren van de integratie van UNIFI in Azure AD, moet u UNIFI uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="97b41-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97b41-125">**Als u wilt toevoegen UNIFI uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="97b41-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97b41-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="97b41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="97b41-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97b41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="97b41-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97b41-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="97b41-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="97b41-133">Typ in het zoekvak **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="97b41-133">In the search box, type **UNIFI**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="97b41-135">Selecteer in het deelvenster resultaten **UNIFI**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="97b41-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97b41-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97b41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97b41-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met UNIFI op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="97b41-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="97b41-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in UNIFI is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97b41-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="97b41-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in UNIFI tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="97b41-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="97b41-141">Wijs in UNIFI, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="97b41-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="97b41-142">Om te configureren en testen van Azure AD eenmalige aanmelding met UNIFI, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="97b41-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97b41-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="97b41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="97b41-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97b41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97b41-145">**[Maken van een UNIFI testgebruiker](#creating-a-unifi-test-user)**  - UNIFI die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="97b41-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="97b41-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="97b41-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97b41-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="97b41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97b41-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="97b41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97b41-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing UNIFI configureren.</span><span class="sxs-lookup"><span data-stu-id="97b41-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="97b41-150">**Voor het configureren van Azure AD eenmalige aanmelding met UNIFI, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="97b41-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="97b41-151">In de Azure-portal op de **UNIFI** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="97b41-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="97b41-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="97b41-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="97b41-155">Op de **UNIFI domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="97b41-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="97b41-157">In de **id** textbox, typ de waarde:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="97b41-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="97b41-158">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="97b41-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="97b41-160">In de **aanmeldings-URL** textbox, typ de URL:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="97b41-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="97b41-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="97b41-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="97b41-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="97b41-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="97b41-165">Op de **UNIFI configuratie** sectie, klikt u op **configureren UNIFI** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="97b41-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="97b41-166">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="97b41-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="97b41-168">In een ander browservenster, meld u aan bij uw **UNIFI** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="97b41-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="97b41-169">Klik op de **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="97b41-169">Click on the **Users**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="97b41-171">Klik op de **toevoegen van nieuwe identiteitsprovider**.</span><span class="sxs-lookup"><span data-stu-id="97b41-171">Click on the **Add New Identity Provider**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="97b41-173">In de **identiteitsprovider toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="97b41-173">In the **Add Identity Provider** section, perform the following steps:</span></span>   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="97b41-175">a.</span><span class="sxs-lookup"><span data-stu-id="97b41-175">a.</span></span> <span data-ttu-id="97b41-176">In de **providernaam** textbox, typ de naam van de identiteitsprovider...</span><span class="sxs-lookup"><span data-stu-id="97b41-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="97b41-177">b.</span><span class="sxs-lookup"><span data-stu-id="97b41-177">b.</span></span> <span data-ttu-id="97b41-178">In de de **Provider URL** textbox plakken de **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="97b41-178">In the the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="97b41-179">c.</span><span class="sxs-lookup"><span data-stu-id="97b41-179">c.</span></span> <span data-ttu-id="97b41-180">Open het certificaat dat u hebt gedownload vanuit de Azure-portal in Kladblok en verwijder de **---BEGIN CERTIFICATE---** en **---EINDCERTIFICAAT---** code en plak vervolgens de resterende inhoud in de **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="97b41-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="97b41-181">d.</span><span class="sxs-lookup"><span data-stu-id="97b41-181">d.</span></span> <span data-ttu-id="97b41-182">Selecteer de **provider is standaard** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="97b41-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="97b41-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="97b41-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="97b41-184">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="97b41-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="97b41-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97b41-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97b41-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="97b41-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="97b41-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="97b41-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="97b41-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="97b41-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97b41-190">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="97b41-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97b41-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="97b41-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97b41-194">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b41-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97b41-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="97b41-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97b41-198">a.</span><span class="sxs-lookup"><span data-stu-id="97b41-198">a.</span></span> <span data-ttu-id="97b41-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97b41-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97b41-200">b.</span><span class="sxs-lookup"><span data-stu-id="97b41-200">b.</span></span> <span data-ttu-id="97b41-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97b41-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97b41-202">c.</span><span class="sxs-lookup"><span data-stu-id="97b41-202">c.</span></span> <span data-ttu-id="97b41-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="97b41-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="97b41-204">d.</span><span class="sxs-lookup"><span data-stu-id="97b41-204">d.</span></span> <span data-ttu-id="97b41-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="97b41-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="97b41-206">Een testgebruiker UNIFI maken</span><span class="sxs-lookup"><span data-stu-id="97b41-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="97b41-207">In deze sectie maakt u een gebruiker met de naam Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97b41-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="97b41-208">**UNIFI** ondersteunt automatische gebruikersaanvragen zodat er geen handmatige stappen vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="97b41-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="97b41-209">Gebruikers worden automatisch gemaakt na een geslaagde authenticatie van de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97b41-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="97b41-210">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="97b41-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="97b41-211">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan UNIFI.</span><span class="sxs-lookup"><span data-stu-id="97b41-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="97b41-213">**Britta Simon om aan te wijzen UNIFI, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="97b41-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="97b41-214">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97b41-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="97b41-216">Selecteer in de lijst met toepassingen **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="97b41-216">In the applications list, select **UNIFI**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="97b41-218">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="97b41-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="97b41-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="97b41-220">Click **Add** button.</span></span> <span data-ttu-id="97b41-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b41-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="97b41-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="97b41-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="97b41-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b41-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97b41-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b41-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97b41-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97b41-226">Testing single sign-on</span></span>

<span data-ttu-id="97b41-227">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="97b41-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="97b41-228">Als u op de tegel UNIFI in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing UNIFI.</span><span class="sxs-lookup"><span data-stu-id="97b41-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="97b41-229">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="97b41-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="97b41-230">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="97b41-230">Additional resources</span></span>

* [<span data-ttu-id="97b41-231">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97b41-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97b41-232">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97b41-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

