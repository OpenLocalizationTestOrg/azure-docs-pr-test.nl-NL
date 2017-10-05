---
title: 'Zelfstudie: Azure Active Directory-integratie met Softeon WMS | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Softeon WMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 07c5de0d-90aa-43b3-b24e-0cc334b2f9b0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jeedes
ms.openlocfilehash: 87714bbcb317395563033d2f0ebc60aaa0ff0e10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-softeon-wms"></a><span data-ttu-id="c55f2-103">Zelfstudie: Azure Active Directory-integratie met Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="c55f2-103">Tutorial: Azure Active Directory integration with Softeon WMS</span></span>

<span data-ttu-id="c55f2-104">In deze zelfstudie leert u hoe Softeon WMS integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c55f2-104">In this tutorial, you learn how to integrate Softeon WMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c55f2-105">Softeon WMS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c55f2-105">Integrating Softeon WMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c55f2-106">U kunt beheren in Azure AD die toegang tot Softeon WMS heeft</span><span class="sxs-lookup"><span data-stu-id="c55f2-106">You can control in Azure AD who has access to Softeon WMS</span></span>
- <span data-ttu-id="c55f2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Softeon WMS (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c55f2-107">You can enable your users to automatically get signed-on to Softeon WMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c55f2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c55f2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c55f2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c55f2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c55f2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c55f2-110">Prerequisites</span></span>

<span data-ttu-id="c55f2-111">Voor het configureren van Azure AD-integratie met Softeon WMS, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c55f2-111">To configure Azure AD integration with Softeon WMS, you need the following items:</span></span>

- <span data-ttu-id="c55f2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c55f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c55f2-113">Een Softeon WMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c55f2-113">A Softeon WMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c55f2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c55f2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c55f2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c55f2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c55f2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c55f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c55f2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c55f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c55f2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c55f2-118">Scenario description</span></span>
<span data-ttu-id="c55f2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c55f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c55f2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c55f2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c55f2-121">Softeon WMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c55f2-121">Adding Softeon WMS from the gallery</span></span>
2. <span data-ttu-id="c55f2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c55f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-softeon-wms-from-the-gallery"></a><span data-ttu-id="c55f2-123">Softeon WMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c55f2-123">Adding Softeon WMS from the gallery</span></span>
<span data-ttu-id="c55f2-124">Voor het configureren van de integratie van Softeon WMS in Azure AD, moet u Softeon WMS uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c55f2-124">To configure the integration of Softeon WMS into Azure AD, you need to add Softeon WMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c55f2-125">**Als u wilt toevoegen Softeon WMS uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c55f2-125">**To add Softeon WMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c55f2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c55f2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c55f2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c55f2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c55f2-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c55f2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c55f2-133">Typ in het zoekvak **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-133">In the search box, type **Softeon WMS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_search.png)

5. <span data-ttu-id="c55f2-135">Selecteer in het deelvenster resultaten **Softeon WMS**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c55f2-135">In the results panel, select **Softeon WMS**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c55f2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c55f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c55f2-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Softeon WMS op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c55f2-138">In this section, you configure and test Azure AD single sign-on with Softeon WMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c55f2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Softeon WMS is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c55f2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Softeon WMS is to a user in Azure AD.</span></span> <span data-ttu-id="c55f2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Softeon WMS tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c55f2-140">In other words, a link relationship between an Azure AD user and the related user in Softeon WMS needs to be established.</span></span>

<span data-ttu-id="c55f2-141">Wijs in Softeon WMS, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c55f2-141">In Softeon WMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c55f2-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Softeon WMS, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c55f2-142">To configure and test Azure AD single sign-on with Softeon WMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c55f2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c55f2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c55f2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c55f2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c55f2-145">**[Maken van een testgebruiker Softeon WMS](#creating-a-softeon-wms-test-user)**  - Softeon WMS die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c55f2-145">**[Creating a Softeon WMS test user](#creating-a-softeon-wms-test-user)** - to have a counterpart of Britta Simon in Softeon WMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c55f2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c55f2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c55f2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c55f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c55f2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c55f2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c55f2-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="c55f2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Softeon WMS application.</span></span>

<span data-ttu-id="c55f2-150">**Voor het configureren van Azure AD eenmalige aanmelding met Softeon WMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c55f2-150">**To configure Azure AD single sign-on with Softeon WMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c55f2-151">In de Azure-portal op de **Softeon WMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-151">In the Azure portal, on the **Softeon WMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c55f2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c55f2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_samlbase.png)

3. <span data-ttu-id="c55f2-155">Op de **Softeon WMS domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c55f2-155">On the **Softeon WMS Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_url.png)

    <span data-ttu-id="c55f2-157">a.</span><span class="sxs-lookup"><span data-stu-id="c55f2-157">a.</span></span> <span data-ttu-id="c55f2-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.softeon.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c55f2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/<instancename>`</span></span>

    <span data-ttu-id="c55f2-159">b.</span><span class="sxs-lookup"><span data-stu-id="c55f2-159">b.</span></span> <span data-ttu-id="c55f2-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.softeon.com/sp`</span><span class="sxs-lookup"><span data-stu-id="c55f2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c55f2-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c55f2-161">These values are not real.</span></span> <span data-ttu-id="c55f2-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="c55f2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c55f2-163">Neem contact op met [Softeon WMS Client ondersteuningsteam](mailto:contact@softeon.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c55f2-163">Contact [Softeon WMS Client support team](mailto:contact@softeon.com) to get these values.</span></span> 
 
4. <span data-ttu-id="c55f2-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c55f2-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_certificate.png) 

5. <span data-ttu-id="c55f2-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c55f2-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-softeon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c55f2-168">Op de **Softeon WMS configuratie** sectie, klikt u op **configureren Softeon WMS** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c55f2-168">On the **Softeon WMS Configuration** section, click **Configure Softeon WMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c55f2-169">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c55f2-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_configure.png) 

7. <span data-ttu-id="c55f2-171">Eenmalige aanmelding configureren op **Softeon WMS** zijde, moet u de gedownloade verzenden **certificaat (Base64), SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [Softeon WMS ondersteuningsteam](mailto:contact@softeon.com).</span><span class="sxs-lookup"><span data-stu-id="c55f2-171">To configure single sign-on on **Softeon WMS** side, you need to send the downloaded **Certificate (Base64), SAML Entity ID, and SAML Single Sign-On Service URL** to [Softeon WMS support team](mailto:contact@softeon.com).</span></span> <span data-ttu-id="c55f2-172">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c55f2-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c55f2-173">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c55f2-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c55f2-174">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c55f2-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c55f2-175">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c55f2-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c55f2-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c55f2-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c55f2-177">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c55f2-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c55f2-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c55f2-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c55f2-180">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c55f2-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-softeon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c55f2-182">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-softeon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c55f2-184">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c55f2-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-softeon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c55f2-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c55f2-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-softeon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c55f2-188">a.</span><span class="sxs-lookup"><span data-stu-id="c55f2-188">a.</span></span> <span data-ttu-id="c55f2-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c55f2-190">b.</span><span class="sxs-lookup"><span data-stu-id="c55f2-190">b.</span></span> <span data-ttu-id="c55f2-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c55f2-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c55f2-192">c.</span><span class="sxs-lookup"><span data-stu-id="c55f2-192">c.</span></span> <span data-ttu-id="c55f2-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c55f2-194">d.</span><span class="sxs-lookup"><span data-stu-id="c55f2-194">d.</span></span> <span data-ttu-id="c55f2-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-195">Click **Create**.</span></span>
 
### <a name="creating-a-softeon-wms-test-user"></a><span data-ttu-id="c55f2-196">Maken van een testgebruiker Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="c55f2-196">Creating a Softeon WMS test user</span></span>

<span data-ttu-id="c55f2-197">Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="c55f2-197">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c55f2-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c55f2-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c55f2-199">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="c55f2-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Softeon WMS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c55f2-201">**Britta Simon om aan te wijzen Softeon WMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c55f2-201">**To assign Britta Simon to Softeon WMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c55f2-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c55f2-204">Selecteer in de lijst met toepassingen **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-204">In the applications list, select **Softeon WMS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_app.png) 

3. <span data-ttu-id="c55f2-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c55f2-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c55f2-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c55f2-208">Click **Add** button.</span></span> <span data-ttu-id="c55f2-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c55f2-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c55f2-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c55f2-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c55f2-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c55f2-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c55f2-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c55f2-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c55f2-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c55f2-214">Testing single sign-on</span></span>

<span data-ttu-id="c55f2-215">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c55f2-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c55f2-216">Als u op de tegel Softeon WMS in het deelvenster toegang, krijgt u de aanmeldingspagina van Softeon WMS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c55f2-216">When you click the Softeon WMS tile in the Access Panel, you should get login page of Softeon WMS application.</span></span>
<span data-ttu-id="c55f2-217">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c55f2-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c55f2-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c55f2-218">Additional resources</span></span>

* [<span data-ttu-id="c55f2-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c55f2-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c55f2-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c55f2-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_203.png

