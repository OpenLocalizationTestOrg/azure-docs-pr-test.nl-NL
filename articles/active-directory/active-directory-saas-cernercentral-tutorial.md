---
title: 'Zelfstudie: Azure Active Directory-integratie met centraal Cerner | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Cerner centraal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="6d191-103">Zelfstudie: Azure Active Directory-integratie met Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="6d191-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="6d191-104">In deze zelfstudie leert u hoe Cerner centraal integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d191-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d191-105">Cerner centraal integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6d191-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d191-106">U kunt beheren in Azure AD die toegang tot Cerner-centraal heeft</span><span class="sxs-lookup"><span data-stu-id="6d191-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="6d191-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Cerner centraal (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="6d191-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d191-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6d191-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6d191-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d191-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d191-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6d191-110">Prerequisites</span></span>

<span data-ttu-id="6d191-111">Voor het configureren van Azure AD-integratie met centraal Cerner, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6d191-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="6d191-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6d191-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d191-113">Een goedgekeurde Cerner centrale systeemaccount</span><span class="sxs-lookup"><span data-stu-id="6d191-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="6d191-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d191-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d191-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6d191-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d191-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6d191-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d191-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d191-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d191-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6d191-118">Scenario description</span></span>
<span data-ttu-id="6d191-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d191-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d191-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6d191-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d191-121">Cerner centraal uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d191-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="6d191-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d191-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="6d191-123">Cerner centraal uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d191-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="6d191-124">Voor het configureren van de integratie van Cerner centraal in Azure AD, moet u centraal Cerner uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6d191-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d191-125">**Als u wilt toevoegen Cerner centraal uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d191-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d191-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d191-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d191-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d191-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d191-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d191-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6d191-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven op het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d191-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6d191-133">Typ in het zoekvak **Cerner centraal**.</span><span class="sxs-lookup"><span data-stu-id="6d191-133">In the search box, type **Cerner Central**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="6d191-135">Selecteer in het deelvenster resultaten **Cerner centraal**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d191-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d191-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d191-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d191-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Cerner centraal op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6d191-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6d191-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Cerner centraal is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d191-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="6d191-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Cerner centrale tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6d191-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="6d191-141">Om te configureren en testen van Azure AD eenmalige aanmelding met Cerner centraal, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6d191-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d191-142">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d191-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d191-143">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d191-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d191-144">**[Maken van een testgebruiker Cerner centraal](#creating-a-cerner-central-test-user)**  - Cerner centraal die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6d191-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="6d191-145">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6d191-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d191-146">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6d191-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d191-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6d191-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d191-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Cerner centraal configureren.</span><span class="sxs-lookup"><span data-stu-id="6d191-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="6d191-149">**Voor het configureren van Azure AD eenmalige aanmelding met Cerner centraal, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d191-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="6d191-150">In de Azure-portal op de **Cerner centraal** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6d191-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6d191-152">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6d191-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="6d191-154">Op de **Cerner centrale domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d191-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="6d191-156">a.</span><span class="sxs-lookup"><span data-stu-id="6d191-156">a.</span></span> <span data-ttu-id="6d191-157">In de **id** textbox, typ de waarde die met behulp van de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="6d191-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="6d191-158">b.</span><span class="sxs-lookup"><span data-stu-id="6d191-158">b.</span></span> <span data-ttu-id="6d191-159">In de **antwoord-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="6d191-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="6d191-160">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="6d191-160">These values are not the real.</span></span> <span data-ttu-id="6d191-161">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="6d191-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6d191-162">Neem contact op met [Cerner centraal ondersteuningsteam](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6d191-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="6d191-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6d191-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="6d191-165">Voor het genereren van de **metagegevens** -url, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6d191-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="6d191-166">a.</span><span class="sxs-lookup"><span data-stu-id="6d191-166">a.</span></span> <span data-ttu-id="6d191-167">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="6d191-167">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="6d191-169">b.</span><span class="sxs-lookup"><span data-stu-id="6d191-169">b.</span></span> <span data-ttu-id="6d191-170">Klik op **eindpunten** openen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d191-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="6d191-172">c.</span><span class="sxs-lookup"><span data-stu-id="6d191-172">c.</span></span> <span data-ttu-id="6d191-173">Klik op de knop kopiëren om te kopiëren **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="6d191-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="6d191-175">d.</span><span class="sxs-lookup"><span data-stu-id="6d191-175">d.</span></span> <span data-ttu-id="6d191-176">Nu gaat u naar de eigenschappenpagina van **Cerner centraal** en kopieer de **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="6d191-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="6d191-178">e.</span><span class="sxs-lookup"><span data-stu-id="6d191-178">e.</span></span> <span data-ttu-id="6d191-179">Genereren van de **metagegevens-URL** met het volgende patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="6d191-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="6d191-180">Eenmalige aanmelding configureren op **Cerner centraal** kant die u wilt verzenden de **metagegevens-URL** naar [Cerner centraal ondersteuning](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="6d191-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="6d191-181">Ze configureren met SSO zijde van de toepassing aan de integratie worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="6d191-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="6d191-182">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6d191-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6d191-183">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6d191-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6d191-184">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d191-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d191-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6d191-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d191-186">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6d191-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6d191-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d191-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d191-189">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d191-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d191-191">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6d191-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d191-193">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6d191-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d191-195">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d191-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d191-197">a.</span><span class="sxs-lookup"><span data-stu-id="6d191-197">a.</span></span> <span data-ttu-id="6d191-198">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d191-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d191-199">b.</span><span class="sxs-lookup"><span data-stu-id="6d191-199">b.</span></span> <span data-ttu-id="6d191-200">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d191-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="6d191-201">c.</span><span class="sxs-lookup"><span data-stu-id="6d191-201">c.</span></span> <span data-ttu-id="6d191-202">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6d191-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d191-203">d.</span><span class="sxs-lookup"><span data-stu-id="6d191-203">d.</span></span> <span data-ttu-id="6d191-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6d191-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="6d191-205">Maken van een testgebruiker Cerner-centraal</span><span class="sxs-lookup"><span data-stu-id="6d191-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="6d191-206">**Cerner centraal** toepassing kunt verificatie van elke provider federatieve identiteiten.</span><span class="sxs-lookup"><span data-stu-id="6d191-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="6d191-207">Als een gebruiker zich kan aanmelden bij de startpagina van de toepassing, wordt deze federatieve zijn en niet nodig is voor handmatige inrichting.</span><span class="sxs-lookup"><span data-stu-id="6d191-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d191-208">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d191-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d191-209">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Cerner centraal.</span><span class="sxs-lookup"><span data-stu-id="6d191-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6d191-211">**Britta Simon om aan te wijzen Cerner centraal, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d191-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="6d191-212">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d191-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6d191-214">Selecteer in de lijst met toepassingen **Cerner centraal**.</span><span class="sxs-lookup"><span data-stu-id="6d191-214">In the applications list, select **Cerner Central**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="6d191-216">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6d191-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6d191-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6d191-218">Click **Add** button.</span></span> <span data-ttu-id="6d191-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d191-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6d191-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6d191-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d191-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d191-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d191-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d191-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d191-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d191-224">Testing single sign-on</span></span>

<span data-ttu-id="6d191-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6d191-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6d191-226">Als u op de tegel Cerner centraal in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Cerner centraal.</span><span class="sxs-lookup"><span data-stu-id="6d191-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="6d191-227">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d191-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d191-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6d191-228">Additional resources</span></span>

* [<span data-ttu-id="6d191-229">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d191-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d191-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d191-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

