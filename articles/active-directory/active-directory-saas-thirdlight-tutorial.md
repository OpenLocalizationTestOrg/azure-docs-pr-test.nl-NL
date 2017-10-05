---
title: 'Zelfstudie: Azure Active Directory-integratie met ThirdLight | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ThirdLight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="d9d67-103">Zelfstudie: Azure Active Directory-integratie met ThirdLight</span><span class="sxs-lookup"><span data-stu-id="d9d67-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="d9d67-104">In deze zelfstudie leert u hoe ThirdLight integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9d67-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9d67-105">ThirdLight integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d9d67-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9d67-106">U kunt beheren in Azure AD die toegang tot ThirdLight heeft</span><span class="sxs-lookup"><span data-stu-id="d9d67-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="d9d67-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ThirdLight (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d9d67-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9d67-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d9d67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d9d67-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9d67-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9d67-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9d67-110">Prerequisites</span></span>

<span data-ttu-id="d9d67-111">Voor het configureren van Azure AD-integratie met ThirdLight, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d9d67-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="d9d67-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d9d67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9d67-113">Een ThirdLight eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d9d67-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9d67-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d9d67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9d67-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d9d67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9d67-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d9d67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9d67-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9d67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9d67-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d9d67-118">Scenario description</span></span>
<span data-ttu-id="d9d67-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d9d67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9d67-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d9d67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9d67-121">ThirdLight uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d9d67-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="d9d67-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d9d67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="d9d67-123">ThirdLight uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d9d67-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="d9d67-124">Voor het configureren van de integratie van ThirdLight in Azure AD, moet u ThirdLight uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d9d67-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9d67-125">**Als u wilt toevoegen ThirdLight uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d9d67-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d67-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d9d67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9d67-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9d67-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d9d67-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9d67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d9d67-133">Typ in het zoekvak **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-133">In the search box, type **ThirdLight**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="d9d67-135">Selecteer in het deelvenster resultaten **ThirdLight**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d9d67-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9d67-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d9d67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9d67-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ThirdLight op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d9d67-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9d67-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ThirdLight is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9d67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="d9d67-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ThirdLight tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d9d67-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="d9d67-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="d9d67-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="d9d67-142">Om te configureren en testen van Azure AD eenmalige aanmelding met ThirdLight, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d9d67-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9d67-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9d67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9d67-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9d67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9d67-145">**[Maken van een testgebruiker ThirdLight](#creating-a-thirdlight-test-user)**  - ThirdLight die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d9d67-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9d67-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d9d67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9d67-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d9d67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9d67-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d9d67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9d67-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ThirdLight configureren.</span><span class="sxs-lookup"><span data-stu-id="d9d67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="d9d67-150">**Voor het configureren van Azure AD eenmalige aanmelding met ThirdLight, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d9d67-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d67-151">In de Azure-portal op de **ThirdLight** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d9d67-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d9d67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="d9d67-155">Op de **ThirdLight domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d9d67-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="d9d67-157">a.</span><span class="sxs-lookup"><span data-stu-id="d9d67-157">a.</span></span> <span data-ttu-id="d9d67-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="d9d67-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="d9d67-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9d67-159">b.</span></span> <span data-ttu-id="d9d67-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="d9d67-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9d67-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="d9d67-161">These values are not real.</span></span> <span data-ttu-id="d9d67-162">Deze waarden met de werkelijke aanmeldings-URL en Identiifer bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d9d67-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="d9d67-163">Neem contact op met [ThirdLight Client ondersteuningsteam](https://www.thirdlight.com/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d9d67-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="d9d67-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d9d67-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="d9d67-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d9d67-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9d67-168">In een ander browservenster, meld u aan bij uw bedrijf ThirdLight site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d9d67-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="d9d67-169">Ga naar **configuratie \> Systeembeheer**, en klik vervolgens op **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="d9d67-170">![Systeembeheer](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="d9d67-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="d9d67-171">Voer de volgende stappen uit in de configuratiesectie SAML2:</span><span class="sxs-lookup"><span data-stu-id="d9d67-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="d9d67-172">![Eenmalige aanmelding SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="d9d67-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="d9d67-173">a.</span><span class="sxs-lookup"><span data-stu-id="d9d67-173">a.</span></span> <span data-ttu-id="d9d67-174">Selecteer **eenmalige aanmelding SAML2 inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="d9d67-175">b.</span><span class="sxs-lookup"><span data-stu-id="d9d67-175">b.</span></span> <span data-ttu-id="d9d67-176">Als **bron voor IdP metagegevens**, selecteer **IdP-metagegevens laden van XML**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="d9d67-177">c.</span><span class="sxs-lookup"><span data-stu-id="d9d67-177">c.</span></span> <span data-ttu-id="d9d67-178">Openen van het metagegevensbestand van de gedownloade, de inhoud kopieert en plakt u deze in de **IdP metagegevens-XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="d9d67-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="d9d67-179">d.</span><span class="sxs-lookup"><span data-stu-id="d9d67-179">d.</span></span> <span data-ttu-id="d9d67-180">Klik op **instellingen opslaan SAML2**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="d9d67-181">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d9d67-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9d67-182">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d9d67-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9d67-183">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9d67-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9d67-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d9d67-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9d67-185">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d9d67-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d9d67-187">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d9d67-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d67-188">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d9d67-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9d67-190">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9d67-192">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9d67-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9d67-194">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d9d67-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9d67-196">a.</span><span class="sxs-lookup"><span data-stu-id="d9d67-196">a.</span></span> <span data-ttu-id="d9d67-197">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9d67-198">b.</span><span class="sxs-lookup"><span data-stu-id="d9d67-198">b.</span></span> <span data-ttu-id="d9d67-199">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9d67-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d9d67-200">c.</span><span class="sxs-lookup"><span data-stu-id="d9d67-200">c.</span></span> <span data-ttu-id="d9d67-201">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d9d67-202">d.</span><span class="sxs-lookup"><span data-stu-id="d9d67-202">d.</span></span> <span data-ttu-id="d9d67-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="d9d67-204">Een testgebruiker ThirdLight maken</span><span class="sxs-lookup"><span data-stu-id="d9d67-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="d9d67-205">Om Azure AD-gebruikers zich aanmelden bij ThirdLight, moeten ze worden ingericht in ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="d9d67-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="d9d67-206">In het geval van ThirdLight is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="d9d67-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="d9d67-207">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d9d67-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d67-208">Meld u aan bij uw **ThirdLight** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d9d67-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="d9d67-209">Ga naar **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d9d67-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="d9d67-210">Selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="d9d67-211">Klik op **nieuwe gebruiker toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d9d67-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="d9d67-212">Voer **de gebruikersnaam, naam of beschrijving, E-mail, kiest u een vooraf ingestelde of groep van nieuwe leden** van een geldige AAD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="d9d67-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="d9d67-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="d9d67-214">U kunt andere Thirdlight gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Thirdlight aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="d9d67-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d9d67-215">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9d67-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d9d67-216">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="d9d67-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d9d67-218">**Britta Simon om aan te wijzen ThirdLight, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d9d67-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="d9d67-219">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d9d67-221">Selecteer in de lijst met toepassingen **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-221">In the applications list, select **ThirdLight**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="d9d67-223">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d9d67-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d9d67-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d9d67-225">Click **Add** button.</span></span> <span data-ttu-id="d9d67-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9d67-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d9d67-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d9d67-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9d67-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9d67-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9d67-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9d67-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9d67-231">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d9d67-231">Testing single sign-on</span></span>

<span data-ttu-id="d9d67-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d9d67-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d9d67-233">Als u op de tegel ThirdLight in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="d9d67-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="d9d67-234">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9d67-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d9d67-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d9d67-235">Additional resources</span></span>

* [<span data-ttu-id="d9d67-236">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9d67-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9d67-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9d67-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

