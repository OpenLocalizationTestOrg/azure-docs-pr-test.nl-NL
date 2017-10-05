---
title: 'Zelfstudie: Azure Active Directory-integratie met Schoolbord meer - Shibboleth | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Schoolbord meer - Shibboleth.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 014b0671eb8604235a823c2cf4324a49d94df702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="6ce2b-103">Zelfstudie: Azure Active Directory-integratie met Schoolbord meer - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="6ce2b-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="6ce2b-104">In deze zelfstudie leert u hoe integreren Schoolbord meer - Shibboleth met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ce2b-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ce2b-105">Integratie van Schoolbord meer - Shibboleth met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6ce2b-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ce2b-106">U kunt beheren in Azure AD die toegang tot Schoolbord meer - Shibboleth heeft</span><span class="sxs-lookup"><span data-stu-id="6ce2b-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="6ce2b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Schoolbord meer - Shibboleth (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6ce2b-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ce2b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6ce2b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6ce2b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ce2b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ce2b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ce2b-110">Prerequisites</span></span>

<span data-ttu-id="6ce2b-111">Voor het configureren van Azure AD-integratie met Schoolbord meer - Shibboleth, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6ce2b-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

- <span data-ttu-id="6ce2b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6ce2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ce2b-113">A meer Schoolbord - Shibboleth eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6ce2b-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ce2b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ce2b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6ce2b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ce2b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ce2b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ce2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ce2b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6ce2b-118">Scenario description</span></span>
<span data-ttu-id="6ce2b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ce2b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6ce2b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ce2b-121">Meer Schoolbord - Shibboleth uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6ce2b-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
2. <span data-ttu-id="6ce2b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ce2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="6ce2b-123">Meer Schoolbord - Shibboleth uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6ce2b-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="6ce2b-124">Om de integratie van Schoolbord meer - Shibboleth met Azure AD te configureren die u wilt toevoegen Schoolbord meer - Shibboleth uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ce2b-125">**Als u wilt toevoegen Schoolbord meer - Shibboleth uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ce2b-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ce2b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ce2b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ce2b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6ce2b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6ce2b-133">Typ in het zoekvak **Schoolbord meer - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-133">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="6ce2b-135">Selecteer in het deelvenster resultaten **Schoolbord meer - Shibboleth**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ce2b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ce2b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ce2b-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Schoolbord meer - Shibboleth op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6ce2b-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6ce2b-139">Azure AD moet weten wat de equivalente gebruiker in Schoolbord meer - Shibboleth is voor een gebruiker in Azure AD voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="6ce2b-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Schoolbord meer - Shibboleth moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="6ce2b-141">Wijs in Schoolbord meer - Shibboleth, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6ce2b-142">Als u wilt configureren en testen Azure AD eenmalige aanmelding met Schoolbord meer - Shibboleth, moet u de volgende elementen voltooid:</span><span class="sxs-lookup"><span data-stu-id="6ce2b-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ce2b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ce2b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ce2b-145">**[Maken van een Schoolbord meer - testgebruiker Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - Schoolbord meer - Shibboleth die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ce2b-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ce2b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ce2b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6ce2b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ce2b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw Schoolbord meer - Shibboleth toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="6ce2b-150">**Voor het configureren van Azure AD eenmalige aanmelding met Schoolbord meer - Shibboleth, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ce2b-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="6ce2b-151">In de Azure-portal op de **Schoolbord meer - Shibboleth** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6ce2b-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="6ce2b-155">Op de **Schoolbord meer - URL's en Shibboleth domein** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ce2b-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="6ce2b-157">a.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-157">a.</span></span> <span data-ttu-id="6ce2b-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="6ce2b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="6ce2b-159">b.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-159">b.</span></span> <span data-ttu-id="6ce2b-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="6ce2b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="6ce2b-161">c.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-161">c.</span></span> <span data-ttu-id="6ce2b-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="6ce2b-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="6ce2b-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-163">These values are not real.</span></span> <span data-ttu-id="6ce2b-164">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6ce2b-165">Neem contact op met [Schoolbord meer - ondersteuningsteam Shibboleth Client](https://www.blackboard.com/forms/contact-us_form.aspx) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span></span> 

4. <span data-ttu-id="6ce2b-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="6ce2b-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6ce2b-170">Op de **Schoolbord meer - Shibboleth configuratie** sectie, klikt u op **configureren Schoolbord meer - Shibboleth** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6ce2b-171">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6ce2b-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="6ce2b-173">Eenmalige aanmelding configureren op **Schoolbord meer - Shibboleth** zijde, moet u de gedownloade verzenden **Metadata XML** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**  naar [Schoolbord meer - ondersteuningsteam Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ce2b-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="6ce2b-174">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6ce2b-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6ce2b-175">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6ce2b-176">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ce2b-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ce2b-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6ce2b-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ce2b-178">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6ce2b-180">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ce2b-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ce2b-181">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ce2b-183">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ce2b-185">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ce2b-187">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6ce2b-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ce2b-189">a.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-189">a.</span></span> <span data-ttu-id="6ce2b-190">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ce2b-191">b.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-191">b.</span></span> <span data-ttu-id="6ce2b-192">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ce2b-193">c.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-193">c.</span></span> <span data-ttu-id="6ce2b-194">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6ce2b-195">d.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-195">d.</span></span> <span data-ttu-id="6ce2b-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="6ce2b-197">Maken van een Schoolbord meer - Shibboleth testgebruiker</span><span class="sxs-lookup"><span data-stu-id="6ce2b-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="6ce2b-198">In deze sectie kunt u een gebruiker met de naam van Britta Simon in Schoolbord meer - Shibboleth maken.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="6ce2b-199">Werken met uw [Schoolbord meer - ondersteuningsteam Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) toevoegen van de gebruikers in de Schoolbord meer - Shibboleth platform.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6ce2b-200">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ce2b-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6ce2b-201">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen voor Schoolbord meer - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6ce2b-203">**Als u wilt toewijzen Britta Simon voor Schoolbord meer - Shibboleth, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6ce2b-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="6ce2b-204">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6ce2b-206">Selecteer in de lijst met toepassingen **Schoolbord meer - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="6ce2b-208">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6ce2b-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-210">Click **Add** button.</span></span> <span data-ttu-id="6ce2b-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6ce2b-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ce2b-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ce2b-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ce2b-216">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6ce2b-216">Testing single sign-on</span></span>

<span data-ttu-id="6ce2b-217">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6ce2b-218">Wanneer u klikt op de Schoolbord meer - tegel in het deelvenster toegang Shibboleth u moet ophalen automatisch aangemeld bij uw Schoolbord meer - Shibboleth toepassing.</span><span class="sxs-lookup"><span data-stu-id="6ce2b-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ce2b-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6ce2b-219">Additional resources</span></span>

* [<span data-ttu-id="6ce2b-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ce2b-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ce2b-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6ce2b-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

