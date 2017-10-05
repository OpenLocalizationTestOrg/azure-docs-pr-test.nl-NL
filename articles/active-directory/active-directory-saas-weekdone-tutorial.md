---
title: 'Zelfstudie: Azure Active Directory-integratie met Weekdone | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Weekdone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 84aa0069dce55a6623398a99e1cac6bb21bf52f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="1c68b-103">Zelfstudie: Azure Active Directory-integratie met Weekdone</span><span class="sxs-lookup"><span data-stu-id="1c68b-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="1c68b-104">In deze zelfstudie leert u hoe Weekdone integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c68b-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c68b-105">Weekdone integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1c68b-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c68b-106">U kunt beheren in Azure AD die toegang tot Weekdone heeft</span><span class="sxs-lookup"><span data-stu-id="1c68b-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="1c68b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Weekdone (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1c68b-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c68b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1c68b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1c68b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c68b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c68b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1c68b-110">Prerequisites</span></span>

<span data-ttu-id="1c68b-111">Voor het configureren van Azure AD-integratie met Weekdone, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1c68b-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="1c68b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1c68b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c68b-113">Een Weekdone eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1c68b-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c68b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1c68b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c68b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1c68b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c68b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1c68b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c68b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c68b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c68b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1c68b-118">Scenario description</span></span>
<span data-ttu-id="1c68b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1c68b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c68b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1c68b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c68b-121">Weekdone uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c68b-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="1c68b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c68b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="1c68b-123">Weekdone uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c68b-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="1c68b-124">Voor het configureren van de integratie van Weekdone in Azure AD, moet u Weekdone uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1c68b-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c68b-125">**Als u wilt toevoegen Weekdone uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c68b-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c68b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1c68b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c68b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c68b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1c68b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c68b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1c68b-133">Typ in het zoekvak **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-133">In the search box, type **Weekdone**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="1c68b-135">Selecteer in het deelvenster resultaten **Weekdone**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c68b-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c68b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c68b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c68b-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Weekdone op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1c68b-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c68b-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Weekdone is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c68b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="1c68b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Weekdone tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1c68b-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="1c68b-141">Wijs in Weekdone, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1c68b-141">In Weekdone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1c68b-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Weekdone, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1c68b-142">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c68b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c68b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1c68b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c68b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c68b-145">**[Maken van een testgebruiker Weekdone](#creating-a-weekdone-test-user)**  - Weekdone die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1c68b-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c68b-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1c68b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c68b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1c68b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c68b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1c68b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c68b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Weekdone configureren.</span><span class="sxs-lookup"><span data-stu-id="1c68b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="1c68b-150">**Voor het configureren van Azure AD eenmalige aanmelding met Weekdone, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c68b-150">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="1c68b-151">In de Azure-portal op de **Weekdone** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-151">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1c68b-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1c68b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="1c68b-155">Op de **Weekdone domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="1c68b-155">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="1c68b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c68b-157">a.</span></span> <span data-ttu-id="1c68b-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="1c68b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="1c68b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c68b-159">b.</span></span> <span data-ttu-id="1c68b-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="1c68b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="1c68b-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1c68b-162">Als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="1c68b-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="1c68b-164">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="1c68b-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1c68b-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1c68b-165">These values are not real.</span></span> <span data-ttu-id="1c68b-166">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="1c68b-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1c68b-167">Neem contact op met [Weekdone Client ondersteuningsteam](mailto:hello@weekdone.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1c68b-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="1c68b-168">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1c68b-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="1c68b-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1c68b-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1c68b-172">Op de **Weekdone configuratie** sectie, klikt u op **configureren Weekdone** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1c68b-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1c68b-173">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1c68b-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="1c68b-175">Eenmalige aanmelding configureren op **Weekdone** zijde, moet u de gedownloade verzenden **Metadata XML, Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [Weekdone ondersteuningsteam ](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="1c68b-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="1c68b-176">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1c68b-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1c68b-177">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1c68b-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1c68b-178">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c68b-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c68b-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1c68b-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c68b-180">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1c68b-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1c68b-182">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c68b-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c68b-183">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1c68b-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c68b-185">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c68b-187">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c68b-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c68b-189">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1c68b-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c68b-191">a.</span><span class="sxs-lookup"><span data-stu-id="1c68b-191">a.</span></span> <span data-ttu-id="1c68b-192">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c68b-193">b.</span><span class="sxs-lookup"><span data-stu-id="1c68b-193">b.</span></span> <span data-ttu-id="1c68b-194">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1c68b-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c68b-195">c.</span><span class="sxs-lookup"><span data-stu-id="1c68b-195">c.</span></span> <span data-ttu-id="1c68b-196">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c68b-197">d.</span><span class="sxs-lookup"><span data-stu-id="1c68b-197">d.</span></span> <span data-ttu-id="1c68b-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="1c68b-199">Een testgebruiker Weekdone maken</span><span class="sxs-lookup"><span data-stu-id="1c68b-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="1c68b-200">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Weekdone genoemd.</span><span class="sxs-lookup"><span data-stu-id="1c68b-200">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="1c68b-201">Weekdone ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1c68b-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1c68b-202">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="1c68b-202">There is no action item for you in this section.</span></span> <span data-ttu-id="1c68b-203">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot Weekdone als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="1c68b-203">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1c68b-204">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Weekdone Client ondersteuningsteam](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="1c68b-204">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1c68b-205">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c68b-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1c68b-206">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Weekdone.</span><span class="sxs-lookup"><span data-stu-id="1c68b-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1c68b-208">**Britta Simon om aan te wijzen Weekdone, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c68b-208">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="1c68b-209">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1c68b-211">Selecteer in de lijst met toepassingen **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-211">In the applications list, select **Weekdone**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="1c68b-213">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1c68b-213">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1c68b-215">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1c68b-215">Click **Add** button.</span></span> <span data-ttu-id="1c68b-216">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c68b-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1c68b-218">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1c68b-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1c68b-219">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c68b-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c68b-220">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c68b-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c68b-221">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c68b-221">Testing single sign-on</span></span>

<span data-ttu-id="1c68b-222">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1c68b-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1c68b-223">Als u op de tegel Weekdone in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Weekdone.</span><span class="sxs-lookup"><span data-stu-id="1c68b-223">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c68b-224">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1c68b-224">Additional resources</span></span>

* [<span data-ttu-id="1c68b-225">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c68b-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c68b-226">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c68b-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

