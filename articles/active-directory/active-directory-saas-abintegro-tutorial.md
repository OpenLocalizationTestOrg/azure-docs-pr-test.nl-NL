---
title: 'Zelfstudie: Azure Active Directory-integratie met Abintegro | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Abintegro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: a2a3c1a7a338ee1cb35dd08176ad3bb5f3cdc319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="93e9c-103">Zelfstudie: Azure Active Directory-integratie met Abintegro</span><span class="sxs-lookup"><span data-stu-id="93e9c-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="93e9c-104">In deze zelfstudie leert u hoe Abintegro integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93e9c-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93e9c-105">Abintegro integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="93e9c-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="93e9c-106">U kunt beheren in Azure AD die toegang tot Abintegro heeft</span><span class="sxs-lookup"><span data-stu-id="93e9c-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="93e9c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Abintegro (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="93e9c-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93e9c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="93e9c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="93e9c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93e9c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93e9c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="93e9c-110">Prerequisites</span></span>

<span data-ttu-id="93e9c-111">Voor het configureren van Azure AD-integratie met Abintegro, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="93e9c-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="93e9c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="93e9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93e9c-113">Een Abintegro eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="93e9c-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93e9c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="93e9c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93e9c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="93e9c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93e9c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="93e9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93e9c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93e9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93e9c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="93e9c-118">Scenario description</span></span>
<span data-ttu-id="93e9c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="93e9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93e9c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="93e9c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93e9c-121">Abintegro uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="93e9c-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="93e9c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="93e9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="93e9c-123">Abintegro uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="93e9c-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="93e9c-124">Voor het configureren van de integratie van Abintegro in Azure AD, moet u Abintegro uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="93e9c-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="93e9c-125">**Als u wilt toevoegen Abintegro uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="93e9c-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="93e9c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="93e9c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93e9c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="93e9c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="93e9c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="93e9c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="93e9c-133">Typ in het zoekvak **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-133">In the search box, type **Abintegro**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="93e9c-135">Selecteer in het deelvenster resultaten **Abintegro**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="93e9c-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93e9c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="93e9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93e9c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Abintegro op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="93e9c-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="93e9c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Abintegro is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93e9c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="93e9c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Abintegro tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="93e9c-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="93e9c-141">Wijs in Abintegro, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="93e9c-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="93e9c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Abintegro, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="93e9c-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="93e9c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="93e9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="93e9c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93e9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93e9c-145">**[Maken van een testgebruiker Abintegro](#creating-an-abintegro-test-user)**  - Abintegro die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="93e9c-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="93e9c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="93e9c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93e9c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="93e9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93e9c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="93e9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93e9c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Abintegro configureren.</span><span class="sxs-lookup"><span data-stu-id="93e9c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="93e9c-150">**Voor het configureren van Azure AD eenmalige aanmelding met Abintegro, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="93e9c-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="93e9c-151">In de Azure-portal op de **Abintegro** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="93e9c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="93e9c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="93e9c-155">Op de **Abintegro domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="93e9c-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="93e9c-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="93e9c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="93e9c-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="93e9c-158">This value is not real.</span></span> <span data-ttu-id="93e9c-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="93e9c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="93e9c-160">Neem contact op met [Abintegro Client ondersteuningsteam](mailto:support@abintegro.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="93e9c-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="93e9c-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="93e9c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="93e9c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="93e9c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93e9c-165">Eenmalige aanmelding configureren op **Abintegro** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Abintegro ondersteuningsteam](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="93e9c-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="93e9c-166">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="93e9c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="93e9c-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="93e9c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="93e9c-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="93e9c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="93e9c-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93e9c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93e9c-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="93e9c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="93e9c-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="93e9c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="93e9c-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="93e9c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="93e9c-174">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="93e9c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93e9c-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93e9c-178">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="93e9c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93e9c-180">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="93e9c-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93e9c-182">a.</span><span class="sxs-lookup"><span data-stu-id="93e9c-182">a.</span></span> <span data-ttu-id="93e9c-183">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93e9c-184">b.</span><span class="sxs-lookup"><span data-stu-id="93e9c-184">b.</span></span> <span data-ttu-id="93e9c-185">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="93e9c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93e9c-186">c.</span><span class="sxs-lookup"><span data-stu-id="93e9c-186">c.</span></span> <span data-ttu-id="93e9c-187">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="93e9c-188">d.</span><span class="sxs-lookup"><span data-stu-id="93e9c-188">d.</span></span> <span data-ttu-id="93e9c-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="93e9c-190">Een testgebruiker Abintegro maken</span><span class="sxs-lookup"><span data-stu-id="93e9c-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="93e9c-191">Er is geen actie-item voor gebruikers inrichten voor Abintegro configuratie.</span><span class="sxs-lookup"><span data-stu-id="93e9c-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="93e9c-192">Wanneer een toegewezen gebruiker probeert aan te melden bij met het toegangsvenster Abintegro, Abintegro u controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="93e9c-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="93e9c-193">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Abintegro.</span><span class="sxs-lookup"><span data-stu-id="93e9c-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="93e9c-194">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="93e9c-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="93e9c-195">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Abintegro.</span><span class="sxs-lookup"><span data-stu-id="93e9c-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="93e9c-197">**Britta Simon om aan te wijzen Abintegro, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="93e9c-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="93e9c-198">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="93e9c-200">Selecteer in de lijst met toepassingen **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-200">In the applications list, select **Abintegro**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="93e9c-202">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="93e9c-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="93e9c-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="93e9c-204">Click **Add** button.</span></span> <span data-ttu-id="93e9c-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="93e9c-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="93e9c-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="93e9c-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="93e9c-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="93e9c-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93e9c-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="93e9c-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93e9c-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="93e9c-210">Testing single sign-on</span></span>

<span data-ttu-id="93e9c-211">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="93e9c-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="93e9c-212">Als u op de tegel Abintegro in het deelvenster toegang, krijgt u de aanmeldingspagina van Abintegro toepassing.</span><span class="sxs-lookup"><span data-stu-id="93e9c-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="93e9c-213">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="93e9c-213">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="93e9c-214">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="93e9c-214">Additional resources</span></span>

* [<span data-ttu-id="93e9c-215">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93e9c-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93e9c-216">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="93e9c-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

