---
title: 'Zelfstudie: Azure Active Directory-integratie met Datahug | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Datahug.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="092c1-103">Zelfstudie: Azure Active Directory-integratie met Datahug</span><span class="sxs-lookup"><span data-stu-id="092c1-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="092c1-104">In deze zelfstudie leert u hoe Datahug integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="092c1-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="092c1-105">Datahug integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="092c1-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="092c1-106">U kunt beheren in Azure AD die toegang tot Datahug heeft</span><span class="sxs-lookup"><span data-stu-id="092c1-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="092c1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Datahug (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="092c1-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="092c1-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="092c1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="092c1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, zien.</span><span class="sxs-lookup"><span data-stu-id="092c1-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="092c1-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="092c1-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="092c1-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="092c1-111">Prerequisites</span></span>

<span data-ttu-id="092c1-112">Voor het configureren van Azure AD-integratie met Datahug, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="092c1-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="092c1-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="092c1-113">An Azure AD subscription</span></span>
- <span data-ttu-id="092c1-114">Een Datahug eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="092c1-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="092c1-115">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="092c1-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="092c1-116">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="092c1-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="092c1-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="092c1-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="092c1-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="092c1-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="092c1-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="092c1-119">Scenario description</span></span>
<span data-ttu-id="092c1-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="092c1-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="092c1-121">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="092c1-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="092c1-122">Datahug uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="092c1-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="092c1-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="092c1-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="092c1-124">Datahug uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="092c1-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="092c1-125">Voor het configureren van de integratie van Datahug in Azure AD, moet u Datahug uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="092c1-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="092c1-126">**Als u wilt toevoegen Datahug uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="092c1-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="092c1-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="092c1-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="092c1-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="092c1-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="092c1-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="092c1-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="092c1-132">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="092c1-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="092c1-134">Typ in het zoekvak **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="092c1-134">In the search box, type **Datahug**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="092c1-136">Selecteer in het deelvenster resultaten **Datahug**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="092c1-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="092c1-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="092c1-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="092c1-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Datahug op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="092c1-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="092c1-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Datahug is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="092c1-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="092c1-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Datahug tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="092c1-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="092c1-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Datahug.</span><span class="sxs-lookup"><span data-stu-id="092c1-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="092c1-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Datahug, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="092c1-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="092c1-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="092c1-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="092c1-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="092c1-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="092c1-146">**[Maken van een testgebruiker Datahug](#creating-a-datahug-test-user)**  - Datahug die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="092c1-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="092c1-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="092c1-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="092c1-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="092c1-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="092c1-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="092c1-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="092c1-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Datahug configureren.</span><span class="sxs-lookup"><span data-stu-id="092c1-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="092c1-151">**Voor het configureren van Azure AD eenmalige aanmelding met Datahug, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="092c1-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="092c1-152">In de Azure-portal op de **Datahug** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="092c1-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="092c1-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="092c1-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="092c1-156">Op de **Datahug domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="092c1-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="092c1-158">a.</span><span class="sxs-lookup"><span data-stu-id="092c1-158">a.</span></span> <span data-ttu-id="092c1-159">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="092c1-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="092c1-160">b.</span><span class="sxs-lookup"><span data-stu-id="092c1-160">b.</span></span> <span data-ttu-id="092c1-161">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="092c1-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="092c1-162">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="092c1-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="092c1-163">Als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="092c1-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="092c1-165">In de **aanmeldings-URL** textbox, typ een URL als:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="092c1-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="092c1-166">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="092c1-166">These values are not the real.</span></span> <span data-ttu-id="092c1-167">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="092c1-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="092c1-168">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="092c1-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="092c1-169">Neem contact op met [Datahug Client ondersteuningsteam](http://datahug.com/about/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="092c1-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="092c1-170">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="092c1-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="092c1-172">Controleer **'Weergeven geavanceerde instellingen voor het ondertekenen van certificaat'** en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="092c1-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="092c1-174">a.</span><span class="sxs-lookup"><span data-stu-id="092c1-174">a.</span></span> <span data-ttu-id="092c1-175">In **ondertekening optie**, selecteer **aanmelding SAML-verklaring**.</span><span class="sxs-lookup"><span data-stu-id="092c1-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="092c1-176">b.</span><span class="sxs-lookup"><span data-stu-id="092c1-176">b.</span></span> <span data-ttu-id="092c1-177">In **ondertekening algoritme**, selecteer **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="092c1-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="092c1-178">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="092c1-178">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="092c1-180">Op de **Datahug configuratie** sectie, klikt u op **configureren Datahug** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="092c1-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="092c1-181">Kopieer de **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="092c1-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="092c1-183">Eenmalige aanmelding configureren op **Datahug** zijde, moet u de gedownloade verzenden **Metadata XML**, **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** naar [Datahug ondersteuning](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="092c1-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="092c1-184">Ze hebben de SAML SSO-verbinding juist ingesteld voor beide zijden van deze toepassing ingesteld.</span><span class="sxs-lookup"><span data-stu-id="092c1-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="092c1-185">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="092c1-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="092c1-186">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="092c1-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="092c1-187">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="092c1-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="092c1-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="092c1-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="092c1-189">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="092c1-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="092c1-191">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="092c1-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="092c1-192">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="092c1-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="092c1-194">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="092c1-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="092c1-196">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="092c1-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="092c1-198">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="092c1-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="092c1-200">a.</span><span class="sxs-lookup"><span data-stu-id="092c1-200">a.</span></span> <span data-ttu-id="092c1-201">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="092c1-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="092c1-202">b.</span><span class="sxs-lookup"><span data-stu-id="092c1-202">b.</span></span> <span data-ttu-id="092c1-203">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="092c1-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="092c1-204">c.</span><span class="sxs-lookup"><span data-stu-id="092c1-204">c.</span></span> <span data-ttu-id="092c1-205">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="092c1-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="092c1-206">d.</span><span class="sxs-lookup"><span data-stu-id="092c1-206">d.</span></span> <span data-ttu-id="092c1-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="092c1-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="092c1-208">Een testgebruiker Datahug maken</span><span class="sxs-lookup"><span data-stu-id="092c1-208">Creating a Datahug test user</span></span>

<span data-ttu-id="092c1-209">Om Azure AD-gebruikers zich aanmelden bij Datahug, moeten ze worden ingericht in Datahug.</span><span class="sxs-lookup"><span data-stu-id="092c1-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="092c1-210">Datahug, inrichting wanneer een handmatige taak is.</span><span class="sxs-lookup"><span data-stu-id="092c1-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="092c1-211">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="092c1-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="092c1-212">Meld u aan bij uw bedrijf Datahug site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="092c1-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="092c1-213">Beweeg de muisaanwijzer over de **tandwiel** in de rechterbovenhoek en klik op **instellingen**</span><span class="sxs-lookup"><span data-stu-id="092c1-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="092c1-215">Kies **mensen** en klik op de **gebruikers toevoegen** tabblad</span><span class="sxs-lookup"><span data-stu-id="092c1-215">Choose **People** and click the **Add Users** tab</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="092c1-217">Typ het e-mailadres van degene die u wilt maken voor een account en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="092c1-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="092c1-219">U kunt registratie-e-mail naar gebruiker verzenden door te selecteren **verzenden welkomstbericht** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="092c1-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="092c1-220">Als u een account voor Salesforce het welkomstbericht niet verzenden.</span><span class="sxs-lookup"><span data-stu-id="092c1-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="092c1-221">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="092c1-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="092c1-222">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Datahug.</span><span class="sxs-lookup"><span data-stu-id="092c1-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="092c1-224">**Britta Simon om aan te wijzen Datahug, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="092c1-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="092c1-225">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="092c1-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="092c1-227">Selecteer in de lijst met toepassingen **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="092c1-227">In the applications list, select **Datahug**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="092c1-229">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="092c1-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="092c1-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="092c1-231">Click **Add** button.</span></span> <span data-ttu-id="092c1-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="092c1-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="092c1-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="092c1-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="092c1-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="092c1-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="092c1-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="092c1-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="092c1-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="092c1-237">Testing single sign-on</span></span>

<span data-ttu-id="092c1-238">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="092c1-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="092c1-239">Als u op de tegel Datahug in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Datahug.</span><span class="sxs-lookup"><span data-stu-id="092c1-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="092c1-240">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="092c1-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="092c1-241">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="092c1-241">Additional resources</span></span>

* [<span data-ttu-id="092c1-242">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="092c1-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="092c1-243">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="092c1-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

