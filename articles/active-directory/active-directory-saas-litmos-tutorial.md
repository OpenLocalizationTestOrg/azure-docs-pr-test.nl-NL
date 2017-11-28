---
title: 'Zelfstudie: Azure Active Directory-integratie met Litmos | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Litmos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ef1b5860ba0a406022bbd11afb366d14bee2c57d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="9a758-103">Zelfstudie: Azure Active Directory-integratie met Litmos</span><span class="sxs-lookup"><span data-stu-id="9a758-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="9a758-104">In deze zelfstudie leert u hoe Litmos integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a758-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a758-105">Litmos integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9a758-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a758-106">U kunt beheren in Azure AD die toegang tot Litmos heeft.</span><span class="sxs-lookup"><span data-stu-id="9a758-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="9a758-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Litmos (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a758-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9a758-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="9a758-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9a758-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a758-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a758-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9a758-110">Prerequisites</span></span>

<span data-ttu-id="9a758-111">Voor het configureren van Azure AD-integratie met Litmos, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9a758-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="9a758-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9a758-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a758-113">Een Litmos eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9a758-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a758-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9a758-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a758-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9a758-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a758-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9a758-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a758-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a758-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a758-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a758-118">Scenario description</span></span>
<span data-ttu-id="9a758-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9a758-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a758-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9a758-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a758-121">Litmos uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a758-121">Adding Litmos from the gallery</span></span>
2. <span data-ttu-id="9a758-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a758-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="9a758-123">Litmos uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a758-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="9a758-124">Voor het configureren van de integratie van Litmos in Azure AD, moet u Litmos uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9a758-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a758-125">**Als u wilt toevoegen Litmos uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a758-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a758-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9a758-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="9a758-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a758-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a758-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a758-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="9a758-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a758-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="9a758-133">Typ in het zoekvak **Litmos**, selecteer **Litmos** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a758-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![Litmos in de lijst met resultaten](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a758-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a758-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a758-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Litmos op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9a758-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a758-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Litmos is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a758-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="9a758-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Litmos tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9a758-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="9a758-139">Wijs in Litmos, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9a758-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9a758-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Litmos, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9a758-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a758-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9a758-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a758-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a758-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a758-143">**[Maak een testgebruiker Litmos](#create-a-litmos-test-user)**  - Litmos die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9a758-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a758-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a758-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a758-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9a758-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a758-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9a758-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a758-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Litmos configureren.</span><span class="sxs-lookup"><span data-stu-id="9a758-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="9a758-148">**Voor het configureren van Azure AD eenmalige aanmelding met Litmos, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a758-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="9a758-149">In de Azure-portal op de **Litmos** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9a758-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9a758-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9a758-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="9a758-153">Op de **Litmos domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9a758-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en Litmos domein eenmalige aanmelding informatie](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="9a758-155">a.</span><span class="sxs-lookup"><span data-stu-id="9a758-155">a.</span></span> <span data-ttu-id="9a758-156">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="9a758-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="9a758-157">b.</span><span class="sxs-lookup"><span data-stu-id="9a758-157">b.</span></span> <span data-ttu-id="9a758-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="9a758-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a758-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="9a758-159">These values are not real.</span></span> <span data-ttu-id="9a758-160">Deze waarden bijwerken met de werkelijke id en de antwoord-URL, die worden beschreven verderop in de zelfstudie of neem contact op met [Litmos ondersteuningsteam](https://www.litmos.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9a758-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="9a758-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9a758-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="9a758-163">Als onderdeel van de configuratie, moet u voor het aanpassen van de **SAML-Token kenmerken** voor uw toepassing Litmos.</span><span class="sxs-lookup"><span data-stu-id="9a758-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![Kenmerk-sectie](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="9a758-165">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="9a758-165">Attribute Name</span></span>   | <span data-ttu-id="9a758-166">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="9a758-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="9a758-167">Voornaam</span><span class="sxs-lookup"><span data-stu-id="9a758-167">FirstName</span></span> |<span data-ttu-id="9a758-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="9a758-168">user.givenname</span></span> |
    | <span data-ttu-id="9a758-169">Achternaam</span><span class="sxs-lookup"><span data-stu-id="9a758-169">LastName</span></span>  |<span data-ttu-id="9a758-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="9a758-170">user.surname</span></span> |
    | <span data-ttu-id="9a758-171">E-mail</span><span class="sxs-lookup"><span data-stu-id="9a758-171">Email</span></span> |<span data-ttu-id="9a758-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="9a758-172">user.mail</span></span> |

    <span data-ttu-id="9a758-173">a.</span><span class="sxs-lookup"><span data-stu-id="9a758-173">a.</span></span> <span data-ttu-id="9a758-174">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a758-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Kenmerk toevoegen](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Kenmerk Dailog toevoegen](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9a758-177">b.</span><span class="sxs-lookup"><span data-stu-id="9a758-177">b.</span></span> <span data-ttu-id="9a758-178">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="9a758-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="9a758-179">c.</span><span class="sxs-lookup"><span data-stu-id="9a758-179">c.</span></span> <span data-ttu-id="9a758-180">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="9a758-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9a758-181">d.</span><span class="sxs-lookup"><span data-stu-id="9a758-181">d.</span></span> <span data-ttu-id="9a758-182">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9a758-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="9a758-183">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9a758-183">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9a758-185">In een ander browservenster aanmelding bij uw bedrijf Litmos site als administrator.</span><span class="sxs-lookup"><span data-stu-id="9a758-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

8. <span data-ttu-id="9a758-186">Klik in de navigatiebalk aan de linkerkant op **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="9a758-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Het gedeelte accounts App-zijde][22] 

9. <span data-ttu-id="9a758-188">Klik op de **integraties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9a758-188">Click the **Integrations** tab.</span></span>
   
    ![Tabblad-integratie][23] 

10. <span data-ttu-id="9a758-190">Op de **integraties** tabblad, schuif omlaag naar **3e partij integraties**, en klik vervolgens op **SAML 2.0** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9a758-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 sectie][24] 

11. <span data-ttu-id="9a758-192">Kopieer de waarde onder **de SAML-eindpunt voor litmos is:** en plak deze in de **antwoord-URL** textbox in de **Litmos domein en de URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9a758-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![SAML-eindpunt][26] 

12. <span data-ttu-id="9a758-194">In uw **Litmos** toepassing, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9a758-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Litmos toepassing][25] 
     
     <span data-ttu-id="9a758-196">a.</span><span class="sxs-lookup"><span data-stu-id="9a758-196">a.</span></span> <span data-ttu-id="9a758-197">Klik op **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="9a758-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="9a758-198">b.</span><span class="sxs-lookup"><span data-stu-id="9a758-198">b.</span></span> <span data-ttu-id="9a758-199">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **SAML X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="9a758-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="9a758-200">c.</span><span class="sxs-lookup"><span data-stu-id="9a758-200">c.</span></span> <span data-ttu-id="9a758-201">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9a758-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="9a758-202">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9a758-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a758-203">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9a758-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a758-204">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a758-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a758-205">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9a758-205">Create an Azure AD test user</span></span>

<span data-ttu-id="9a758-206">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9a758-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="9a758-208">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a758-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a758-209">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="9a758-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9a758-211">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9a758-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9a758-213">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a758-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9a758-215">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9a758-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9a758-217">a.</span><span class="sxs-lookup"><span data-stu-id="9a758-217">a.</span></span> <span data-ttu-id="9a758-218">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a758-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a758-219">b.</span><span class="sxs-lookup"><span data-stu-id="9a758-219">b.</span></span> <span data-ttu-id="9a758-220">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a758-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9a758-221">c.</span><span class="sxs-lookup"><span data-stu-id="9a758-221">c.</span></span> <span data-ttu-id="9a758-222">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="9a758-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9a758-223">d.</span><span class="sxs-lookup"><span data-stu-id="9a758-223">d.</span></span> <span data-ttu-id="9a758-224">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a758-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="9a758-225">Een testgebruiker Litmos maken</span><span class="sxs-lookup"><span data-stu-id="9a758-225">Create a Litmos test user</span></span>

<span data-ttu-id="9a758-226">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Litmos genoemd.</span><span class="sxs-lookup"><span data-stu-id="9a758-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="9a758-227">De toepassing Litmos ondersteunt Just-in-Time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="9a758-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="9a758-228">Dit betekent een gebruikersaccount wordt automatisch gemaakt indien nodig tijdens een poging tot toegang tot de toepassing die het toegangsvenster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9a758-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="9a758-229">**Als u wilt een gebruiker Britta Simon aangeroepen in Litmos maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a758-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="9a758-230">In een ander browservenster aanmelding bij uw bedrijf Litmos site als administrator.</span><span class="sxs-lookup"><span data-stu-id="9a758-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

2. <span data-ttu-id="9a758-231">Klik in de navigatiebalk aan de linkerkant op **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="9a758-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Het gedeelte accounts App-zijde][22] 

3. <span data-ttu-id="9a758-233">Klik op de **integraties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9a758-233">Click the **Integrations** tab.</span></span>
   
    ![Tabblad integraties][23] 

4. <span data-ttu-id="9a758-235">Op de **integraties** tabblad, schuif omlaag naar **3e partij integraties**, en klik vervolgens op **SAML 2.0** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9a758-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="9a758-237">Selecteer **Autogenerate gebruikers**</span><span class="sxs-lookup"><span data-stu-id="9a758-237">Select **Autogenerate Users**</span></span>
   
    ![Gebruikers automatisch genereren][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9a758-239">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="9a758-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="9a758-240">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Litmos.</span><span class="sxs-lookup"><span data-stu-id="9a758-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="9a758-242">**Britta Simon om aan te wijzen Litmos, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9a758-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="9a758-243">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a758-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9a758-245">Selecteer in de lijst met toepassingen **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="9a758-245">In the applications list, select **Litmos**.</span></span>

    ![De koppeling Litmos in de lijst met toepassingen](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="9a758-247">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9a758-247">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="9a758-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9a758-249">Click **Add** button.</span></span> <span data-ttu-id="9a758-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a758-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="9a758-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9a758-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a758-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a758-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a758-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a758-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a758-255">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a758-255">Test single sign-on</span></span>

<span data-ttu-id="9a758-256">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="9a758-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="9a758-257">Als u op de tegel Litmos in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Litmos.</span><span class="sxs-lookup"><span data-stu-id="9a758-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a758-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9a758-258">Additional resources</span></span>

* [<span data-ttu-id="9a758-259">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a758-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a758-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a758-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

