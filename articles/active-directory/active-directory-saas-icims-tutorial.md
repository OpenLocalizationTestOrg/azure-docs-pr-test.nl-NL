---
title: 'Zelfstudie: Azure Active Directory-integratie met ICIMS | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ICIMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 26a6b41a0e59924d007855ca548f22ed00bd7e23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="96eb9-103">Zelfstudie: Azure Active Directory-integratie met ICIMS</span><span class="sxs-lookup"><span data-stu-id="96eb9-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="96eb9-104">In deze zelfstudie leert u hoe ICIMS integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96eb9-104">In this tutorial, you learn how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96eb9-105">ICIMS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="96eb9-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="96eb9-106">U kunt beheren in Azure AD die toegang tot ICIMS heeft</span><span class="sxs-lookup"><span data-stu-id="96eb9-106">You can control in Azure AD who has access to ICIMS</span></span>
- <span data-ttu-id="96eb9-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ICIMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="96eb9-107">You can enable your users to automatically get signed-on to ICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96eb9-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="96eb9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="96eb9-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96eb9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96eb9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="96eb9-110">Prerequisites</span></span>

<span data-ttu-id="96eb9-111">Voor het configureren van Azure AD-integratie met ICIMS, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="96eb9-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

- <span data-ttu-id="96eb9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="96eb9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96eb9-113">Een ICIMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="96eb9-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96eb9-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="96eb9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96eb9-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="96eb9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96eb9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="96eb9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96eb9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96eb9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96eb9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="96eb9-118">Scenario description</span></span>
<span data-ttu-id="96eb9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="96eb9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96eb9-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="96eb9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96eb9-121">ICIMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="96eb9-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="96eb9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="96eb9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-the-gallery"></a><span data-ttu-id="96eb9-123">ICIMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="96eb9-123">Adding ICIMS from the gallery</span></span>
<span data-ttu-id="96eb9-124">Voor het configureren van de integratie van ICIMS in Azure AD, moet u ICIMS uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="96eb9-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="96eb9-125">**Als u wilt toevoegen ICIMS uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96eb9-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="96eb9-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="96eb9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="96eb9-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="96eb9-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="96eb9-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96eb9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="96eb9-133">Typ in het zoekvak **ICIMS**, selecteer **ICIMS** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="96eb9-133">In the search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button to add the application.</span></span>

    ![ICIMS in de lijst met resultaten](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="96eb9-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="96eb9-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="96eb9-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met ICIMS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="96eb9-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96eb9-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ICIMS is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96eb9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ICIMS is to a user in Azure AD.</span></span> <span data-ttu-id="96eb9-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ICIMS tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="96eb9-138">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>

<span data-ttu-id="96eb9-139">Wijs in ICIMS, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="96eb9-139">In ICIMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="96eb9-140">Om te configureren en testen van Azure AD eenmalige aanmelding met ICIMS, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="96eb9-140">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="96eb9-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96eb9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="96eb9-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96eb9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96eb9-143">**[Maken van een testgebruiker ICIMS](#create-an-icims-test-user)**  - ICIMS die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="96eb9-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="96eb9-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="96eb9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96eb9-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="96eb9-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="96eb9-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="96eb9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="96eb9-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ICIMS configureren.</span><span class="sxs-lookup"><span data-stu-id="96eb9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="96eb9-148">**Voor het configureren van Azure AD eenmalige aanmelding met ICIMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96eb9-148">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="96eb9-149">In de Azure-portal op de **ICIMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-149">In the Azure portal, on the **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="96eb9-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="96eb9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="96eb9-153">Op de **ICIMS domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="96eb9-153">On the **ICIMS Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en ICIMS domein eenmalige aanmelding informatie](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="96eb9-155">a.</span><span class="sxs-lookup"><span data-stu-id="96eb9-155">a.</span></span> <span data-ttu-id="96eb9-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="96eb9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="96eb9-157">b.</span><span class="sxs-lookup"><span data-stu-id="96eb9-157">b.</span></span> <span data-ttu-id="96eb9-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="96eb9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96eb9-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="96eb9-159">These values are not real.</span></span> <span data-ttu-id="96eb9-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="96eb9-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="96eb9-161">Neem contact op met [ICIMS Client ondersteuningsteam](https://www.icims.com/contact-us) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="96eb9-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="96eb9-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="96eb9-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="96eb9-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="96eb9-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96eb9-166">Op de **ICIMS configuratie** sectie, klikt u op **configureren ICIMS** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="96eb9-166">On the **ICIMS Configuration** section, click **Configure ICIMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="96eb9-167">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="96eb9-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ICIMS configuratie](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="96eb9-169">Eenmalige aanmelding configureren op **ICIMS** zijde, moet u de gedownloade verzenden **Metadata XML**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [ ICIMS ondersteuningsteam](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="96eb9-169">To configure single sign-on on **ICIMS** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="96eb9-170">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="96eb9-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="96eb9-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="96eb9-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="96eb9-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="96eb9-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="96eb9-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96eb9-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="96eb9-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="96eb9-174">Create an Azure AD test user</span></span>
<span data-ttu-id="96eb9-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="96eb9-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="96eb9-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96eb9-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="96eb9-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="96eb9-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96eb9-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96eb9-182">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96eb9-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96eb9-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="96eb9-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96eb9-186">a.</span><span class="sxs-lookup"><span data-stu-id="96eb9-186">a.</span></span> <span data-ttu-id="96eb9-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96eb9-188">b.</span><span class="sxs-lookup"><span data-stu-id="96eb9-188">b.</span></span> <span data-ttu-id="96eb9-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96eb9-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96eb9-190">c.</span><span class="sxs-lookup"><span data-stu-id="96eb9-190">c.</span></span> <span data-ttu-id="96eb9-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="96eb9-192">d.</span><span class="sxs-lookup"><span data-stu-id="96eb9-192">d.</span></span> <span data-ttu-id="96eb9-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="96eb9-194">Een testgebruiker ICIMS maken</span><span class="sxs-lookup"><span data-stu-id="96eb9-194">Create an ICIMS test user</span></span>

<span data-ttu-id="96eb9-195">Het doel van deze sectie is het maken van een gebruiker Britta Simon in ICIMS genoemd.</span><span class="sxs-lookup"><span data-stu-id="96eb9-195">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="96eb9-196">Werken met [ICIMS ondersteuningsteam](https://www.icims.com/contact-us) de gebruikers in het account ICIMS toevoegen.</span><span class="sxs-lookup"><span data-stu-id="96eb9-196">Work with [ICIMS support team](https://www.icims.com/contact-us) to add the users in the ICIMS account.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="96eb9-197">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="96eb9-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="96eb9-198">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ICIMS.</span><span class="sxs-lookup"><span data-stu-id="96eb9-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ICIMS.</span></span>

![Toewijzen van de gebruikersrol][200]

<span data-ttu-id="96eb9-200">**Britta Simon om aan te wijzen ICIMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="96eb9-200">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="96eb9-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="96eb9-203">Selecteer in de lijst met toepassingen **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-203">In the applications list, select **ICIMS**.</span></span>

    ![De koppeling ICIMS in de lijst met toepassingen](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="96eb9-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="96eb9-205">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202] 

4. <span data-ttu-id="96eb9-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="96eb9-207">Click **Add** button.</span></span> <span data-ttu-id="96eb9-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96eb9-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="96eb9-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="96eb9-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="96eb9-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96eb9-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96eb9-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="96eb9-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="96eb9-213">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="96eb9-213">Test single sign-on</span></span>

<span data-ttu-id="96eb9-214">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="96eb9-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="96eb9-215">Als u op de tegel ICIMS in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ICIMS.</span><span class="sxs-lookup"><span data-stu-id="96eb9-215">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96eb9-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="96eb9-216">Additional resources</span></span>

* [<span data-ttu-id="96eb9-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96eb9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96eb9-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96eb9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

