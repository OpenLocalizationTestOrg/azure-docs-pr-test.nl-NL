---
title: 'Zelfstudie: Azure Active Directory-integratie met de Planning van Predictix assortiment | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Predictix assortiment plannen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: cc7ad4aa5260276e26406b6b79c039372e5ee69f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="5dd8a-103">Zelfstudie: Azure Active Directory-integratie met Predictix assortiment plannen</span><span class="sxs-lookup"><span data-stu-id="5dd8a-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>

<span data-ttu-id="5dd8a-104">In deze zelfstudie leert u hoe Predictix assortimentplanning integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5dd8a-104">In this tutorial, you learn how to integrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5dd8a-105">Predictix assortimentplanning integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-105">Integrating Predictix Assortment Planning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5dd8a-106">U kunt beheren in Azure AD die toegang tot Predictix assortiment plannen heeft.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-106">You can control in Azure AD who has access to Predictix Assortment Planning.</span></span>
- <span data-ttu-id="5dd8a-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Predictix assortiment plannen (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-107">You can enable your users to automatically get signed-on to Predictix Assortment Planning (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5dd8a-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5dd8a-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5dd8a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dd8a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5dd8a-110">Prerequisites</span></span>

<span data-ttu-id="5dd8a-111">Voor het configureren van Azure AD-integratie met de Predictix assortimentplanning, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-111">To configure Azure AD integration with Predictix Assortment Planning, you need the following items:</span></span>

- <span data-ttu-id="5dd8a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5dd8a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5dd8a-113">Een Predictix assortimentplanning eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5dd8a-113">A Predictix Assortment Planning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5dd8a-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5dd8a-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5dd8a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5dd8a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5dd8a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5dd8a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5dd8a-118">Scenario description</span></span>
<span data-ttu-id="5dd8a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5dd8a-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5dd8a-121">Het toevoegen van Predictix assortimentplanning van de galerie</span><span class="sxs-lookup"><span data-stu-id="5dd8a-121">Adding Predictix Assortment Planning from the gallery</span></span>
2. <span data-ttu-id="5dd8a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5dd8a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-assortment-planning-from-the-gallery"></a><span data-ttu-id="5dd8a-123">Het toevoegen van Predictix assortimentplanning van de galerie</span><span class="sxs-lookup"><span data-stu-id="5dd8a-123">Adding Predictix Assortment Planning from the gallery</span></span>
<span data-ttu-id="5dd8a-124">U moet Predictix assortiment plannen uit de galerie aan de lijst met beheerde SaaS-apps toevoegen voor het configureren van de integratie van de Planning van Predictix assortiment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-124">To configure the integration of Predictix Assortment Planning into Azure AD, you need to add Predictix Assortment Planning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5dd8a-125">**Als u wilt toevoegen Predictix assortiment plannen uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5dd8a-125">**To add Predictix Assortment Planning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5dd8a-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="5dd8a-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5dd8a-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="5dd8a-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="5dd8a-133">Typ in het zoekvak **Predictix assortimentplanning**, selecteer **Predictix assortimentplanning** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-133">In the search box, type **Predictix Assortment Planning**, select **Predictix Assortment Planning** from result panel then click **Add** button to add the application.</span></span>

    ![Predictix assortiment plannen in de lijst met resultaten](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5dd8a-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="5dd8a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5dd8a-136">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Predictix assortiment plannen op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="5dd8a-136">In this section, you configure and test Azure AD single sign-on with Predictix Assortment Planning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5dd8a-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de Planning van Predictix assortiment is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Assortment Planning is to a user in Azure AD.</span></span> <span data-ttu-id="5dd8a-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker bij het plannen van Predictix assortiment tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-138">In other words, a link relationship between an Azure AD user and the related user in Predictix Assortment Planning needs to be established.</span></span>

<span data-ttu-id="5dd8a-139">Wijs in het Predictix assortimentplanning, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-139">In Predictix Assortment Planning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5dd8a-140">Om te configureren en testen van Azure AD eenmalige aanmelding met de Predictix assortimentplanning, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-140">To configure and test Azure AD single sign-on with Predictix Assortment Planning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5dd8a-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5dd8a-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5dd8a-143">**[Maak een testgebruiker Predictix assortimentplanning](#create-a-predictix-assortment-planning-test-user)**  - Predictix assortimentplanning die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-143">**[Create a Predictix Assortment Planning test user](#create-a-predictix-assortment-planning-test-user)** - to have a counterpart of Britta Simon in Predictix Assortment Planning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5dd8a-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5dd8a-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5dd8a-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5dd8a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5dd8a-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Predictix assortiment plannen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="5dd8a-148">**Voor het configureren van Azure AD eenmalige aanmelding met de Predictix assortimentplanning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5dd8a-148">**To configure Azure AD single sign-on with Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="5dd8a-149">In de Azure-portal op de **Predictix assortimentplanning** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-149">In the Azure portal, on the **Predictix Assortment Planning** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5dd8a-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. <span data-ttu-id="5dd8a-153">Op de **Predictix assortiment Planning domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-153">On the **Predictix Assortment Planning Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en Predictix assortiment Planning domein eenmalige aanmelding informatie](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    <span data-ttu-id="5dd8a-155">a.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-155">a.</span></span> <span data-ttu-id="5dd8a-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    <span data-ttu-id="5dd8a-157">b.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-157">b.</span></span> <span data-ttu-id="5dd8a-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > <span data-ttu-id="5dd8a-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-159">These values are not real.</span></span> <span data-ttu-id="5dd8a-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5dd8a-161">Neem contact op met [Predictix assortiment Planning Client ondersteuningsteam](http://www.infor.com/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-161">Contact [Predictix Assortment Planning Client support team](http://www.infor.com/support) to get these values.</span></span> 
 


4. <span data-ttu-id="5dd8a-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. <span data-ttu-id="5dd8a-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5dd8a-166">Op de **Predictix assortiment Planning configuratie** sectie, klikt u op **configureren Predictix assortimentplanning** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-166">On the **Predictix Assortment Planning Configuration** section, click **Configure Predictix Assortment Planning** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5dd8a-167">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="5dd8a-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Predictix assortiment Planning configuratie](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. <span data-ttu-id="5dd8a-169">Eenmalige aanmelding configureren op **Predictix assortimentplanning** zijde, moet u de gedownloade verzenden **Certificate(Base64)**, **SAML entiteit-ID**, **SAML Single Sign-On Service-URL**, en **Sign-Out URL** naar [ondersteuningsteam Predictix assortimentplanning](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="5dd8a-169">To configure single sign-on on **Predictix Assortment Planning** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL**  to [Predictix Assortment Planning support team](http://www.infor.com/support).</span></span> <span data-ttu-id="5dd8a-170">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5dd8a-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="5dd8a-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5dd8a-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5dd8a-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5dd8a-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5dd8a-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5dd8a-174">Create an Azure AD test user</span></span>

<span data-ttu-id="5dd8a-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="5dd8a-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5dd8a-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5dd8a-178">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5dd8a-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5dd8a-182">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5dd8a-184">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5dd8a-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5dd8a-186">a.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-186">a.</span></span> <span data-ttu-id="5dd8a-187">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5dd8a-188">b.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-188">b.</span></span> <span data-ttu-id="5dd8a-189">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5dd8a-190">c.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-190">c.</span></span> <span data-ttu-id="5dd8a-191">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5dd8a-192">d.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-192">d.</span></span> <span data-ttu-id="5dd8a-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-assortment-planning-test-user"></a><span data-ttu-id="5dd8a-194">Maak een testgebruiker Predictix assortiment plannen</span><span class="sxs-lookup"><span data-stu-id="5dd8a-194">Create a Predictix Assortment Planning test user</span></span>

<span data-ttu-id="5dd8a-195">In deze sectie maakt u Britta Simon aangeroepen bij het plannen van Predictix assortiment van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-195">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="5dd8a-196">Neem contact op met [ondersteuningsteam Predictix assortimentplanning](http://www.infor.com/contact/) om toe te voegen de gebruikers van het platform Predictix assortiment plannen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-196">Please work with [Predictix Assortment Planning support team](http://www.infor.com/contact/) to add the users in the Predictix Assortment Planning platform.</span></span>
 > [!NOTE]
 > <span data-ttu-id="5dd8a-197">De houder van Azure Active Directory-account ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-197">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5dd8a-198">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="5dd8a-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="5dd8a-199">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot de Predictix assortimentplanning.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Predictix Assortment Planning.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="5dd8a-201">**Als u wilt toewijzen Britta Simon Predictix assortiment planning, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5dd8a-201">**To assign Britta Simon to Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="5dd8a-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5dd8a-204">Selecteer in de lijst met toepassingen **Predictix assortimentplanning**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-204">In the applications list, select **Predictix Assortment Planning**.</span></span>

    ![De koppeling Predictix assortiment plannen in de lijst met toepassingen](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. <span data-ttu-id="5dd8a-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-206">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="5dd8a-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-208">Click **Add** button.</span></span> <span data-ttu-id="5dd8a-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="5dd8a-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5dd8a-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5dd8a-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5dd8a-214">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5dd8a-214">Test single sign-on</span></span>

<span data-ttu-id="5dd8a-215">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5dd8a-216">Als u op de tegel Predictix assortimentplanning in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Predictix assortiment plannen.</span><span class="sxs-lookup"><span data-stu-id="5dd8a-216">When you click the Predictix Assortment Planning tile in the Access Panel, you should get automatically signed-on to your Predictix Assortment Planning application.</span></span>
<span data-ttu-id="5dd8a-217">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5dd8a-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5dd8a-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5dd8a-218">Additional resources</span></span>

* [<span data-ttu-id="5dd8a-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5dd8a-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5dd8a-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5dd8a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

