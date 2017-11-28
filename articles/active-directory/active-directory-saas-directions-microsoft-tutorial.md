---
title: 'Zelfstudie: Azure Active Directory-integratie met instructies voor Microsoft | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en instructies voor Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="aea79-103">Zelfstudie: Azure Active Directory-integratie met instructies voor Microsoft</span><span class="sxs-lookup"><span data-stu-id="aea79-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="aea79-104">In deze zelfstudie leert u hoe instructies over het Microsoft integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aea79-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aea79-105">Instructies over het Microsoft integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="aea79-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aea79-106">U kunt beheren in Azure AD die toegang tot de aanwijzingen op Microsoft heeft</span><span class="sxs-lookup"><span data-stu-id="aea79-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="aea79-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de richtlijnen van Microsoft (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="aea79-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aea79-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="aea79-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aea79-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aea79-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aea79-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aea79-110">Prerequisites</span></span>

<span data-ttu-id="aea79-111">Voor het configureren van Azure AD-integratie met instructies voor Microsoft, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="aea79-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="aea79-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="aea79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aea79-113">Een instructies voor eenmalige aanmelding Microsoft abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="aea79-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aea79-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="aea79-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aea79-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="aea79-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aea79-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="aea79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aea79-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aea79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aea79-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="aea79-118">Scenario description</span></span>
<span data-ttu-id="aea79-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="aea79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aea79-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="aea79-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aea79-121">Instructies voor Microsoft toe te voegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="aea79-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="aea79-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aea79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="aea79-123">Instructies voor Microsoft toe te voegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="aea79-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="aea79-124">Voor het configureren van de integratie van richtingen op Microsoft met Azure AD, moet u instructies voor Microsoft uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="aea79-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aea79-125">**Als u wilt toevoegen richtingen op Microsoft uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aea79-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aea79-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aea79-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aea79-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aea79-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aea79-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aea79-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="aea79-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aea79-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="aea79-133">Typ in het zoekvak **instructies over het Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="aea79-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="aea79-135">Selecteer in het deelvenster resultaten **instructies over het Microsoft**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aea79-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aea79-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aea79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aea79-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met instructies voor Microsoft op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="aea79-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aea79-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in richtingen op Microsoft is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aea79-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="aea79-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker kanten op Microsoft tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="aea79-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="aea79-141">Wijs in richtingen op Microsoft de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="aea79-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aea79-142">Om te configureren en testen van Azure AD eenmalige aanmelding met instructies voor Microsoft, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="aea79-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aea79-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aea79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aea79-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aea79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aea79-145">**[Maken van een richtingen op Microsoft testgebruiker](#creating-a-directions-on-microsoft-test-user)**  - instructies over het Microsoft die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="aea79-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aea79-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="aea79-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aea79-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="aea79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aea79-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="aea79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aea79-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw richtingen op Microsoft-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aea79-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="aea79-150">**Als u wilt met instructies over het Microsoft Azure AD eenmalige aanmelding configureert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aea79-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="aea79-151">In de Azure-portal op de **instructies over het Microsoft** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="aea79-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="aea79-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="aea79-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="aea79-155">Op de **instructies over het Microsoft-Domain en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="aea79-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="aea79-157">a.</span><span class="sxs-lookup"><span data-stu-id="aea79-157">a.</span></span> <span data-ttu-id="aea79-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="aea79-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="aea79-159">b.</span><span class="sxs-lookup"><span data-stu-id="aea79-159">b.</span></span> <span data-ttu-id="aea79-160">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="aea79-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="aea79-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="aea79-161">These values are not real.</span></span> <span data-ttu-id="aea79-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="aea79-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="aea79-163">Neem contact op met [instructies over het Microsoft Client ondersteuningsteam](mailto:service@DirectionsOnMicrosoft.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="aea79-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="aea79-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="aea79-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="aea79-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="aea79-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aea79-168">Eenmalige aanmelding configureren op **instructies over het Microsoft** zijde, moet u de gedownloade verzenden **Metadata XML** naar [instructies over het Microsoft-ondersteuningsteam](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="aea79-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="aea79-169">De instructies op Microsoft ondersteuning om in te schakelen team vinden van uw federatieve sitelidmaatschap, gegevens van uw bedrijf opnemen in uw e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="aea79-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="aea79-170">Eenmalige aanmelding voor instructies over het Microsoft moet worden ingeschakeld door de [instructies over het Microsoft Client ondersteuningsteam](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="aea79-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="aea79-171">U ontvangt een melding wanneer eenmalige aanmelding is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aea79-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="aea79-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="aea79-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aea79-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="aea79-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aea79-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aea79-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aea79-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="aea79-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="aea79-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="aea79-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="aea79-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aea79-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aea79-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aea79-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aea79-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="aea79-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aea79-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aea79-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aea79-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="aea79-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aea79-187">a.</span><span class="sxs-lookup"><span data-stu-id="aea79-187">a.</span></span> <span data-ttu-id="aea79-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aea79-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aea79-189">b.</span><span class="sxs-lookup"><span data-stu-id="aea79-189">b.</span></span> <span data-ttu-id="aea79-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aea79-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aea79-191">c.</span><span class="sxs-lookup"><span data-stu-id="aea79-191">c.</span></span> <span data-ttu-id="aea79-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="aea79-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aea79-193">d.</span><span class="sxs-lookup"><span data-stu-id="aea79-193">d.</span></span> <span data-ttu-id="aea79-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="aea79-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="aea79-195">Maken van een richtingen op Microsoft testgebruiker</span><span class="sxs-lookup"><span data-stu-id="aea79-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="aea79-196">Er is geen actie-item voor gebruikers inrichten voor instructies over het Microsoft configuratie.</span><span class="sxs-lookup"><span data-stu-id="aea79-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="aea79-197">Wanneer een toegewezen gebruiker probeert zich aanmelden bij de aanwijzingen op het toegangsvenster met Microsoft, worden instructies over het Microsoft controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="aea79-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="aea79-198">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door de richtlijnen van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aea79-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aea79-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="aea79-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aea79-200">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang aan de richtlijnen van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aea79-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="aea79-202">**Als u wilt toewijzen Britta Simon voor instructies over het Microsoft, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aea79-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="aea79-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aea79-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="aea79-205">Selecteer in de lijst met toepassingen **instructies over het Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="aea79-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="aea79-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="aea79-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="aea79-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="aea79-209">Click **Add** button.</span></span> <span data-ttu-id="aea79-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aea79-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="aea79-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="aea79-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aea79-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aea79-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aea79-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aea79-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aea79-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aea79-215">Testing single sign-on</span></span>

<span data-ttu-id="aea79-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="aea79-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="aea79-217">Als u de aanwijzingen op Microsoft-tegel in het deelvenster toegang op, u moet ophalen automatisch aangemeld bij uw instructies over het Microsoft-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aea79-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="aea79-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aea79-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aea79-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="aea79-219">Additional resources</span></span>

* [<span data-ttu-id="aea79-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aea79-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aea79-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aea79-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

