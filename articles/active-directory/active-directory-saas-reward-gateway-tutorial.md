---
title: 'Zelfstudie: Azure Active Directory-integratie met derden Gateway | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en derden Gateway.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: b1a468caa22159ad603dbec1ef530e7e0e24f96d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="f1ef3-103">Zelfstudie: Azure Active Directory-integratie met derden Gateway</span><span class="sxs-lookup"><span data-stu-id="f1ef3-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="f1ef3-104">In deze zelfstudie leert u hoe derden Gateway integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1ef3-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1ef3-105">Integratie van derden Gateway in Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1ef3-106">U kunt beheren in Azure AD die toegang tot de Gateway van derden heeft</span><span class="sxs-lookup"><span data-stu-id="f1ef3-106">You can control in Azure AD who has access to Reward Gateway</span></span>
- <span data-ttu-id="f1ef3-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de Gateway derden (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f1ef3-107">You can enable your users to automatically get signed-on to Reward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1ef3-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f1ef3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1ef3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1ef3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1ef3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f1ef3-110">Prerequisites</span></span>

<span data-ttu-id="f1ef3-111">Voor het configureren van Azure AD-integratie met derden Gateway, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span></span>

- <span data-ttu-id="f1ef3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f1ef3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1ef3-113">Een Gateway derden eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f1ef3-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1ef3-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1ef3-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1ef3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1ef3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1ef3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1ef3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f1ef3-118">Scenario description</span></span>
<span data-ttu-id="f1ef3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1ef3-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1ef3-121">Toevoegen van derden Gateway vanuit de galerie</span><span class="sxs-lookup"><span data-stu-id="f1ef3-121">Adding Reward Gateway from the gallery</span></span>
2. <span data-ttu-id="f1ef3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1ef3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-the-gallery"></a><span data-ttu-id="f1ef3-123">Toevoegen van derden Gateway vanuit de galerie</span><span class="sxs-lookup"><span data-stu-id="f1ef3-123">Adding Reward Gateway from the gallery</span></span>
<span data-ttu-id="f1ef3-124">Voor het configureren van de integratie van derden Gateway in Azure AD, moet u derden Gateway vanuit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1ef3-125">**Als u wilt toevoegen derden Gateway vanuit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1ef3-125">**To add Reward Gateway from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1ef3-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1ef3-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1ef3-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f1ef3-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f1ef3-133">Typ in het zoekvak **derden Gateway**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-133">In the search box, type **Reward Gateway**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. <span data-ttu-id="f1ef3-135">Selecteer in het deelvenster resultaten **derden Gateway**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-135">In the results panel, select **Reward Gateway**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1ef3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1ef3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1ef3-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met derden Gateway op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1ef3-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de Gateway van derden is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span></span> <span data-ttu-id="f1ef3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in derden Gateway worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-140">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span></span>

<span data-ttu-id="f1ef3-141">In de Gateway van derden, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-141">In Reward Gateway, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f1ef3-142">Om te configureren en testen van Azure AD eenmalige aanmelding met derden Gateway, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-142">To configure and test Azure AD single sign-on with Reward Gateway, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1ef3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1ef3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1ef3-145">**[Maken van een testgebruiker derden Gateway](#creating-a-reward-gateway-test-user)**  - Gateway van derden die is gekoppeld aan de Azure AD-weergave van de gebruiker van een equivalent van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1ef3-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1ef3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1ef3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f1ef3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1ef3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing van derden Gateway configureren.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="f1ef3-150">**Voor het configureren van Azure AD eenmalige aanmelding met derden Gateway, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1ef3-150">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="f1ef3-151">In de Azure-portal op de **derden Gateway** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-151">In the Azure portal, on the **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f1ef3-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. <span data-ttu-id="f1ef3-155">Op de **URL's en het domein van derden Gateway** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-155">On the **Reward Gateway Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="f1ef3-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-157">a.</span></span> <span data-ttu-id="f1ef3-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="f1ef3-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-159">b.</span></span> <span data-ttu-id="f1ef3-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="f1ef3-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-161">These values are not real.</span></span> <span data-ttu-id="f1ef3-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f1ef3-163">Neem contact op met [ondersteuningsteam van derden Gateway](mailto:clientsupport@rewardgateway.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-163">Contact [Reward Gateway support team](mailto:clientsupport@rewardgateway.com) to get these values.</span></span>
 
4. <span data-ttu-id="f1ef3-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. <span data-ttu-id="f1ef3-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1ef3-168">Eenmalige aanmelding configureren op **derden Gateway** zijde, moet u de gedownloade verzenden **Metadata XML** naar [ondersteuningsteam van derden Gateway](mailto:clientsupport@rewardgateway.com).</span><span class="sxs-lookup"><span data-stu-id="f1ef3-168">To configure single sign-on on **Reward Gateway** side, you need to send the downloaded **Metadata XML** to [Reward Gateway support team](mailto:clientsupport@rewardgateway.com).</span></span> <span data-ttu-id="f1ef3-169">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f1ef3-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f1ef3-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1ef3-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1ef3-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1ef3-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1ef3-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f1ef3-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1ef3-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f1ef3-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1ef3-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1ef3-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1ef3-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1ef3-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1ef3-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f1ef3-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1ef3-185">a.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-185">a.</span></span> <span data-ttu-id="f1ef3-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1ef3-187">b.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-187">b.</span></span> <span data-ttu-id="f1ef3-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1ef3-189">c.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-189">c.</span></span> <span data-ttu-id="f1ef3-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1ef3-191">d.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-191">d.</span></span> <span data-ttu-id="f1ef3-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-192">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="f1ef3-193">Een testgebruiker derden Gateway maken</span><span class="sxs-lookup"><span data-stu-id="f1ef3-193">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="f1ef3-194">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in derden Gateway maken.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-194">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="f1ef3-195">Werken met derden Gateway [ondersteuningsteam](mailto:clientsupport@rewardgateway.com) om toe te voegen de gebruikers van het platform van de Gateway van derden.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-195">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1ef3-196">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ef3-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1ef3-197">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan derden Gateway.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reward Gateway.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f1ef3-199">**Als u wilt toewijzen Britta Simon aan derden Gateway, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f1ef3-199">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="f1ef3-200">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f1ef3-202">Selecteer in de lijst met toepassingen **derden Gateway**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-202">In the applications list, select **Reward Gateway**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. <span data-ttu-id="f1ef3-204">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f1ef3-206">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-206">Click **Add** button.</span></span> <span data-ttu-id="f1ef3-207">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f1ef3-209">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1ef3-210">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1ef3-211">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1ef3-212">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1ef3-212">Testing single sign-on</span></span>

<span data-ttu-id="f1ef3-213">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f1ef3-214">Als u op de tegel derden Gateway in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing van derden Gateway.</span><span class="sxs-lookup"><span data-stu-id="f1ef3-214">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1ef3-215">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f1ef3-215">Additional resources</span></span>

* [<span data-ttu-id="f1ef3-216">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1ef3-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1ef3-217">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1ef3-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png

