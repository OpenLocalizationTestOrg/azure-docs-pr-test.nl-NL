---
title: 'Zelfstudie: Azure Active Directory-integratie met FileCloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FileCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="83d07-103">Zelfstudie: Azure Active Directory-integratie met FileCloud</span><span class="sxs-lookup"><span data-stu-id="83d07-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="83d07-104">In deze zelfstudie leert u hoe toointegrate FileCloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83d07-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83d07-105">FileCloud integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="83d07-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="83d07-106">U kunt beheren in Azure AD die tooFileCloud toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="83d07-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="83d07-107">U kunt uw gebruikers tooautomatically get aangemelde tooFileCloud (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="83d07-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="83d07-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="83d07-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="83d07-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83d07-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83d07-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="83d07-110">Prerequisites</span></span>

<span data-ttu-id="83d07-111">Azure AD-integratie met FileCloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="83d07-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="83d07-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="83d07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83d07-113">Een FileCloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="83d07-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83d07-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="83d07-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83d07-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="83d07-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83d07-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="83d07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83d07-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83d07-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83d07-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="83d07-118">Scenario description</span></span>
<span data-ttu-id="83d07-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="83d07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83d07-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="83d07-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83d07-121">Het toevoegen van FileCloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="83d07-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="83d07-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="83d07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="83d07-123">Het toevoegen van FileCloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="83d07-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="83d07-124">tooconfigure hello integratie van FileCloud in Azure AD, moet u tooadd FileCloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="83d07-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83d07-125">**tooadd FileCloud via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="83d07-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83d07-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="83d07-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="83d07-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="83d07-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="83d07-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="83d07-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="83d07-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83d07-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="83d07-133">Typ in het zoekvak Hallo **FileCloud**, selecteer **FileCloud** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="83d07-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![FileCloud in de lijst met resultaten Hallo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="83d07-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="83d07-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="83d07-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met FileCloud op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="83d07-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83d07-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FileCloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83d07-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="83d07-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in FileCloud toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="83d07-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="83d07-139">Wijs in FileCloud, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="83d07-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="83d07-140">tooconfigure en eenmalige aanmelding Azure AD-test met FileCloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="83d07-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83d07-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="83d07-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83d07-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83d07-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83d07-143">**[Maak een testgebruiker FileCloud](#create-a-filecloud-test-user)**  -toohave een equivalent van Britta Simon in FileCloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="83d07-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="83d07-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="83d07-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83d07-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="83d07-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="83d07-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="83d07-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="83d07-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing FileCloud configureren.</span><span class="sxs-lookup"><span data-stu-id="83d07-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="83d07-148">**Azure AD tooconfigure eenmalige aanmelding met FileCloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="83d07-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="83d07-149">In de Azure-portal op Hallo Hallo **FileCloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="83d07-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="83d07-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="83d07-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="83d07-153">Op Hallo **FileCloud domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="83d07-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en FileCloud domein eenmalige aanmelding informatie](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="83d07-155">a.</span><span class="sxs-lookup"><span data-stu-id="83d07-155">a.</span></span> <span data-ttu-id="83d07-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="83d07-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="83d07-157">b.</span><span class="sxs-lookup"><span data-stu-id="83d07-157">b.</span></span> <span data-ttu-id="83d07-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="83d07-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83d07-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="83d07-159">These values are not real.</span></span> <span data-ttu-id="83d07-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="83d07-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="83d07-161">Neem contact op met [FileCloud Client ondersteuningsteam](mailto:support@codelathe.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="83d07-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="83d07-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="83d07-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="83d07-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="83d07-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="83d07-166">Op Hallo **FileCloud configuratie** sectie, klikt u op **configureren FileCloud** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="83d07-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="83d07-167">Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="83d07-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![FileCloud configuratie](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="83d07-169">In een ander browservenster, aanmelding tooyour FileCloud tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="83d07-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="83d07-170">Klik op Hallo navigatiedeelvenster links **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="83d07-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![Instellingen sectie op App aan clientzijde](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="83d07-172">Klik op **SSO** tabblad op het gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="83d07-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Single Sign-On tabblad op App aan clientzijde](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="83d07-174">Selecteer **SAML** als **SSO standaardtype** op **instellingen voor eenmalige aanmelding op (SSO)** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="83d07-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Single Sign-On Configuratiescherm op App instellingen aan clientzijde](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="83d07-176">Plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal in Hallo **IdP eindpunt-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="83d07-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![IDP End punt URL Textbox](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="83d07-178">Open uw gedownloade metagegevensbestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **IdP metagegevens** textbox op **SAML instellingen** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="83d07-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![IDP Meta gegevenssectie App-zijde](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="83d07-180">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="83d07-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="83d07-181">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="83d07-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="83d07-182">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="83d07-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="83d07-183">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83d07-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="83d07-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="83d07-184">Create an Azure AD test user</span></span>

<span data-ttu-id="83d07-185">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="83d07-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="83d07-187">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="83d07-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83d07-188">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="83d07-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="83d07-190">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="83d07-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="83d07-192">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83d07-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="83d07-194">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="83d07-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="83d07-196">a.</span><span class="sxs-lookup"><span data-stu-id="83d07-196">a.</span></span> <span data-ttu-id="83d07-197">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83d07-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83d07-198">b.</span><span class="sxs-lookup"><span data-stu-id="83d07-198">b.</span></span> <span data-ttu-id="83d07-199">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="83d07-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="83d07-200">c.</span><span class="sxs-lookup"><span data-stu-id="83d07-200">c.</span></span> <span data-ttu-id="83d07-201">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="83d07-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="83d07-202">d.</span><span class="sxs-lookup"><span data-stu-id="83d07-202">d.</span></span> <span data-ttu-id="83d07-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="83d07-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="83d07-204">Een testgebruiker FileCloud maken</span><span class="sxs-lookup"><span data-stu-id="83d07-204">Create a FileCloud test user</span></span>

<span data-ttu-id="83d07-205">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in FileCloud van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="83d07-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="83d07-206">FileCloud ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="83d07-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="83d07-207">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="83d07-207">There is no action item for you in this section.</span></span> <span data-ttu-id="83d07-208">Een nieuwe gebruiker wordt tijdens een poging tooaccess FileCloud gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="83d07-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="83d07-209">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [FileCloud Client ondersteuningsteam](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="83d07-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="83d07-210">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="83d07-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="83d07-211">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooFileCloud toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="83d07-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="83d07-213">**tooassign Britta Simon tooFileCloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="83d07-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="83d07-214">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="83d07-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="83d07-216">Selecteer in de lijst met de toepassingen van Hallo **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="83d07-216">In hello applications list, select **FileCloud**.</span></span>

    ![Hallo FileCloud koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="83d07-218">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="83d07-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="83d07-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="83d07-220">Click **Add** button.</span></span> <span data-ttu-id="83d07-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83d07-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="83d07-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="83d07-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="83d07-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83d07-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83d07-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="83d07-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="83d07-226">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="83d07-226">Test single sign-on</span></span>

<span data-ttu-id="83d07-227">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="83d07-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="83d07-228">Als u op Hallo FileCloud tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour FileCloud toepassing.</span><span class="sxs-lookup"><span data-stu-id="83d07-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83d07-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="83d07-229">Additional resources</span></span>

* [<span data-ttu-id="83d07-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83d07-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83d07-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83d07-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

