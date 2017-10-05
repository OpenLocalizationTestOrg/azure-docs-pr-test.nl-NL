---
title: 'Zelfstudie: Azure Active Directory-integratie met Kindling | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Kindling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 131c2c3f46c60193d512b1779e917c8322732fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="1a92f-103">Zelfstudie: Azure Active Directory-integratie met Kindling</span><span class="sxs-lookup"><span data-stu-id="1a92f-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="1a92f-104">In deze zelfstudie leert u hoe Kindling integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a92f-104">In this tutorial, you learn how to integrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a92f-105">Kindling integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1a92f-105">Integrating Kindling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a92f-106">U kunt beheren in Azure AD die toegang tot Kindling heeft</span><span class="sxs-lookup"><span data-stu-id="1a92f-106">You can control in Azure AD who has access to Kindling</span></span>
- <span data-ttu-id="1a92f-107">U kunt uw gebruikers automatisch aangemeld bij inschakelen Kindling (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="1a92f-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a92f-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1a92f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1a92f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, zien.</span><span class="sxs-lookup"><span data-stu-id="1a92f-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="1a92f-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a92f-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a92f-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a92f-111">Prerequisites</span></span>

<span data-ttu-id="1a92f-112">Voor het configureren van Azure AD-integratie met Kindling, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1a92f-112">To configure Azure AD integration with Kindling, you need the following items:</span></span>

- <span data-ttu-id="1a92f-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1a92f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1a92f-114">Een Kindling eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1a92f-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a92f-115">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a92f-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a92f-116">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1a92f-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a92f-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1a92f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a92f-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a92f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a92f-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1a92f-119">Scenario description</span></span>
<span data-ttu-id="1a92f-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a92f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a92f-121">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1a92f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a92f-122">Kindling uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a92f-122">Adding Kindling from the gallery</span></span>
2. <span data-ttu-id="1a92f-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a92f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-the-gallery"></a><span data-ttu-id="1a92f-124">Kindling uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a92f-124">Adding Kindling from the gallery</span></span>
<span data-ttu-id="1a92f-125">Voor het configureren van de integratie van Kindling met Azure AD, moet u Kindling uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1a92f-125">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a92f-126">**Als u wilt toevoegen Kindling uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a92f-126">**To add Kindling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a92f-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a92f-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a92f-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a92f-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1a92f-132">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a92f-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1a92f-134">Typ in het zoekvak **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-134">In the search box, type **Kindling**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="1a92f-136">Selecteer in het deelvenster resultaten **Kindling**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a92f-136">In the results panel, select **Kindling**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a92f-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a92f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a92f-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Kindling op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1a92f-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1a92f-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Kindling is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a92f-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling is to a user in Azure AD.</span></span> <span data-ttu-id="1a92f-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Kindling tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1a92f-141">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span></span>

<span data-ttu-id="1a92f-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Kindling.</span><span class="sxs-lookup"><span data-stu-id="1a92f-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span></span>

<span data-ttu-id="1a92f-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Kindling, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1a92f-143">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a92f-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a92f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1a92f-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a92f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a92f-146">**[Maken van een testgebruiker Kindling](#creating-a-kindling-test-user)**  - Kindling die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1a92f-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a92f-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a92f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a92f-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1a92f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a92f-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1a92f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a92f-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Kindling configureren.</span><span class="sxs-lookup"><span data-stu-id="1a92f-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="1a92f-151">**Voor het configureren van Azure AD eenmalige aanmelding met Kindling, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a92f-151">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="1a92f-152">In de Azure-portal op de **Kindling** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-152">In the Azure portal, on the **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1a92f-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a92f-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="1a92f-156">Op de **Kindling domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a92f-156">On the **Kindling Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="1a92f-158">a.</span><span class="sxs-lookup"><span data-stu-id="1a92f-158">a.</span></span> <span data-ttu-id="1a92f-159">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="1a92f-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="1a92f-160">b.</span><span class="sxs-lookup"><span data-stu-id="1a92f-160">b.</span></span>  <span data-ttu-id="1a92f-161">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="1a92f-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a92f-162">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="1a92f-162">These values are not the real.</span></span> <span data-ttu-id="1a92f-163">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="1a92f-163">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="1a92f-164">Neem contact op met [Kindling ondersteuningsteam](mailto:support@kindlingapp.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1a92f-164">Contact [Kindling support team](mailto:support@kindlingapp.com) to get these values.</span></span>
 
4. <span data-ttu-id="1a92f-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1a92f-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="1a92f-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1a92f-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a92f-169">Op de **Kindling configuratie** sectie, klikt u op **configureren Kindling** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1a92f-169">On the **Kindling Configuration** section, click **Configure Kindling** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1a92f-170">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1a92f-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="1a92f-172">Eenmalige aanmelding configureren op **Kindling** zijde, moet u de gedownloade verzenden **certificaat (Base64)**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [Kindling ondersteuningsteam](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="1a92f-172">To configure single sign-on on **Kindling** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="1a92f-173">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1a92f-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a92f-174">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1a92f-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a92f-175">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a92f-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a92f-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1a92f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a92f-177">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1a92f-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1a92f-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a92f-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a92f-180">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a92f-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a92f-182">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a92f-184">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a92f-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a92f-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a92f-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a92f-188">a.</span><span class="sxs-lookup"><span data-stu-id="1a92f-188">a.</span></span> <span data-ttu-id="1a92f-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a92f-190">b.</span><span class="sxs-lookup"><span data-stu-id="1a92f-190">b.</span></span> <span data-ttu-id="1a92f-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a92f-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a92f-192">c.</span><span class="sxs-lookup"><span data-stu-id="1a92f-192">c.</span></span> <span data-ttu-id="1a92f-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1a92f-194">d.</span><span class="sxs-lookup"><span data-stu-id="1a92f-194">d.</span></span> <span data-ttu-id="1a92f-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="1a92f-196">Een testgebruiker Kindling maken</span><span class="sxs-lookup"><span data-stu-id="1a92f-196">Creating a Kindling test user</span></span>

<span data-ttu-id="1a92f-197">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Kindling genoemd.</span><span class="sxs-lookup"><span data-stu-id="1a92f-197">The objective of this section is to create a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="1a92f-198">Kindling ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="1a92f-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="1a92f-199">U hebt al ingeschakeld in [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="1a92f-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="1a92f-200">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="1a92f-200">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1a92f-201">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a92f-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1a92f-202">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Kindling.</span><span class="sxs-lookup"><span data-stu-id="1a92f-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kindling.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1a92f-204">**Britta Simon om aan te wijzen Kindling, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a92f-204">**To assign Britta Simon to Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="1a92f-205">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1a92f-207">Selecteer in de lijst met toepassingen **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-207">In the applications list, select **Kindling**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="1a92f-209">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1a92f-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1a92f-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1a92f-211">Click **Add** button.</span></span> <span data-ttu-id="1a92f-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a92f-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1a92f-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a92f-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1a92f-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a92f-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a92f-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a92f-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a92f-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a92f-217">Testing single sign-on</span></span>

<span data-ttu-id="1a92f-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1a92f-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1a92f-219">Als u op de tegel Kindling in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Kindling.</span><span class="sxs-lookup"><span data-stu-id="1a92f-219">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1a92f-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1a92f-220">Additional resources</span></span>

* [<span data-ttu-id="1a92f-221">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a92f-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a92f-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a92f-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

