---
title: 'Zelfstudie: Azure Active Directory-integratie met Insperity ExpensAble | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Insperity ExpensAble.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: b50e10be54b1fc413be10bee5b58631790629335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="b0638-103">Zelfstudie: Azure Active Directory-integratie met Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="b0638-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="b0638-104">In deze zelfstudie leert u hoe Insperity ExpensAble integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0638-104">In this tutorial, you learn how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0638-105">Insperity ExpensAble integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b0638-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b0638-106">U kunt beheren in Azure AD die toegang tot Insperity ExpensAble heeft</span><span class="sxs-lookup"><span data-stu-id="b0638-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
- <span data-ttu-id="b0638-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Insperity ExpensAble (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b0638-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0638-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b0638-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b0638-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0638-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0638-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b0638-110">Prerequisites</span></span>

<span data-ttu-id="b0638-111">Voor het configureren van Azure AD-integratie met Insperity ExpensAble, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b0638-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

- <span data-ttu-id="b0638-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b0638-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0638-113">Een Insperity ExpensAble eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b0638-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0638-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b0638-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0638-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b0638-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0638-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b0638-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0638-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0638-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0638-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b0638-118">Scenario description</span></span>
<span data-ttu-id="b0638-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b0638-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0638-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b0638-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0638-121">Toe te voegen Insperity ExpensAble uit de galerie</span><span class="sxs-lookup"><span data-stu-id="b0638-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="b0638-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0638-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="b0638-123">Toe te voegen Insperity ExpensAble uit de galerie</span><span class="sxs-lookup"><span data-stu-id="b0638-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="b0638-124">Voor het configureren van de integratie van Insperity ExpensAble in Azure AD, moet u Insperity ExpensAble uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b0638-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b0638-125">**Als u wilt toevoegen Insperity ExpensAble uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0638-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b0638-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b0638-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0638-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0638-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b0638-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0638-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b0638-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0638-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b0638-133">Typ in het zoekvak **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="b0638-133">In the search box, type **Insperity ExpensAble**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="b0638-135">Selecteer in het deelvenster resultaten **Insperity ExpensAble**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0638-135">In the results panel, select **Insperity ExpensAble**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0638-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0638-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0638-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Insperity ExpensAble op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b0638-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0638-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Insperity ExpensAble is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0638-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble is to a user in Azure AD.</span></span> <span data-ttu-id="b0638-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Insperity ExpensAble tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b0638-140">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>

<span data-ttu-id="b0638-141">Wijs in Insperity ExpensAble, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b0638-141">In Insperity ExpensAble, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b0638-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Insperity ExpensAble, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b0638-142">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b0638-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0638-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b0638-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0638-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0638-145">**[Maken van een Insperity ExpensAble testgebruiker](#creating-an-insperity-expensable-test-user)**  - bevatten een equivalent van Britta Simon Insperity ExpensAble die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b0638-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0638-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b0638-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0638-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b0638-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0638-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b0638-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0638-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Insperity ExpensAble configureren.</span><span class="sxs-lookup"><span data-stu-id="b0638-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="b0638-150">**Voor het configureren van Azure AD eenmalige aanmelding met Insperity ExpensAble, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0638-150">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="b0638-151">In de Azure-portal op de **Insperity ExpensAble** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b0638-151">In the Azure portal, on the **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b0638-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b0638-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="b0638-155">Op de **Insperity ExpensAble domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b0638-155">On the **Insperity ExpensAble Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="b0638-157">a.</span><span class="sxs-lookup"><span data-stu-id="b0638-157">a.</span></span> <span data-ttu-id="b0638-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="b0638-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0638-159">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="b0638-159">This value is not real.</span></span> <span data-ttu-id="b0638-160">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0638-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b0638-161">Neem contact op met [Insperity ExpensAble Client ondersteuningsteam](http://expensable.com/support/support-overview) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="b0638-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) to get this value.</span></span> 
 
4. <span data-ttu-id="b0638-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b0638-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="b0638-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b0638-164">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0638-166">Op de **Insperity ExpensAble configuratie** sectie, klikt u op **Insperity ExpensAble configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b0638-166">On the **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b0638-167">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b0638-167">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="b0638-169">Eenmalige aanmelding configureren op **Insperity ExpensAble** zijde, moet u de gedownloade verzenden **Metadata XML**, **SAML Single Sign-On Service-URL** en  **Entiteit-ID van SAML** naar [Insperity ExpensAble ondersteuningsteam](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="b0638-169">To configure single sign-on on **Insperity ExpensAble** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="b0638-170">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b0638-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b0638-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b0638-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b0638-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b0638-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b0638-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0638-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0638-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b0638-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0638-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b0638-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b0638-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0638-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b0638-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b0638-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0638-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b0638-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0638-182">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0638-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0638-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b0638-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0638-186">a.</span><span class="sxs-lookup"><span data-stu-id="b0638-186">a.</span></span> <span data-ttu-id="b0638-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0638-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0638-188">b.</span><span class="sxs-lookup"><span data-stu-id="b0638-188">b.</span></span> <span data-ttu-id="b0638-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0638-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0638-190">c.</span><span class="sxs-lookup"><span data-stu-id="b0638-190">c.</span></span> <span data-ttu-id="b0638-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b0638-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b0638-192">d.</span><span class="sxs-lookup"><span data-stu-id="b0638-192">d.</span></span> <span data-ttu-id="b0638-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0638-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="b0638-194">Een Insperity ExpensAble testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b0638-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="b0638-195">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Insperity ExpensAble genoemd.</span><span class="sxs-lookup"><span data-stu-id="b0638-195">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="b0638-196">Neem contact op met [Insperity ExpensAble ondersteuningsteam](http://expensable.com/support/support-overview) de gebruikers in het Insperity ExpensAble account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b0638-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) to add the users in the Insperity ExpensAble account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b0638-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0638-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b0638-198">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b0638-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insperity ExpensAble.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b0638-200">**Britta Simon om aan te wijzen Insperity ExpensAble, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0638-200">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="b0638-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0638-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b0638-203">Selecteer in de lijst met toepassingen **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="b0638-203">In the applications list, select **Insperity ExpensAble**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="b0638-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b0638-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b0638-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b0638-207">Click **Add** button.</span></span> <span data-ttu-id="b0638-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0638-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b0638-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b0638-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b0638-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0638-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0638-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0638-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0638-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0638-213">Testing single sign-on</span></span>

<span data-ttu-id="b0638-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b0638-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b0638-215">Als u op de tegel Insperity ExpensAble in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Insperity ExpensAble toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0638-215">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>
<span data-ttu-id="b0638-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0638-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0638-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b0638-217">Additional resources</span></span>

* [<span data-ttu-id="b0638-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0638-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0638-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0638-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

