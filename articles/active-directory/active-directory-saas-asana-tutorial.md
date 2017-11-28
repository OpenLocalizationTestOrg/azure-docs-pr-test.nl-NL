---
title: 'Zelfstudie: Azure Active Directory-integratie met Asana | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Asana.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="7d5ab-103">Zelfstudie: Azure Active Directory-integratie met Asana</span><span class="sxs-lookup"><span data-stu-id="7d5ab-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="7d5ab-104">In deze zelfstudie leert u hoe toointegrate Asana met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d5ab-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d5ab-105">Asana integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d5ab-106">U kunt beheren in Azure AD die tooAsana toegang heeft</span><span class="sxs-lookup"><span data-stu-id="7d5ab-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="7d5ab-107">U kunt uw gebruikers tooautomatically get aangemelde tooAsana (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7d5ab-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d5ab-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7d5ab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7d5ab-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d5ab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d5ab-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7d5ab-110">Prerequisites</span></span>

<span data-ttu-id="7d5ab-111">Azure AD-integratie met Asana tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="7d5ab-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7d5ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d5ab-113">Een Asana eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7d5ab-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d5ab-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d5ab-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d5ab-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d5ab-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d5ab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d5ab-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7d5ab-118">Scenario description</span></span>
<span data-ttu-id="7d5ab-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d5ab-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d5ab-121">Het toevoegen van Asana van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7d5ab-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="7d5ab-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7d5ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="7d5ab-123">Het toevoegen van Asana van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7d5ab-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="7d5ab-124">tooconfigure hello integratie van Asana in Azure AD, moet u tooadd Asana uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d5ab-125">**tooadd Asana via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7d5ab-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d5ab-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="7d5ab-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7d5ab-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="7d5ab-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="7d5ab-133">Typ in het zoekvak Hallo **Asana**, selecteer **Asana** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7d5ab-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d5ab-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7d5ab-136">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Asana op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7d5ab-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7d5ab-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Asana is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="7d5ab-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Asana toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="7d5ab-139">Wijs in Asana, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7d5ab-140">tooconfigure en eenmalige aanmelding Azure AD-test met Asana, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d5ab-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d5ab-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d5ab-143">**[Maken van een testgebruiker Asana](#create-an-asana-test-user)**  -toohave een equivalent van Britta Simon in Asana die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d5ab-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d5ab-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7d5ab-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7d5ab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7d5ab-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Asana configureren.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="7d5ab-148">**Azure AD tooconfigure eenmalige aanmelding met Asana, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7d5ab-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d5ab-149">In de Azure-portal op Hallo Hallo **Asana** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7d5ab-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="7d5ab-153">Op Hallo **Asana domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Asana domein eenmalige aanmelding informatie](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="7d5ab-155">a.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-155">a.</span></span> <span data-ttu-id="7d5ab-156">In Hallo **aanmeldings-URL** textbox, typ de URL:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="7d5ab-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="7d5ab-157">b.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-157">b.</span></span> <span data-ttu-id="7d5ab-158">In Hallo **id** textbox typewaarde:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="7d5ab-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="7d5ab-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="7d5ab-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7d5ab-163">Op Hallo **Asana configuratie** sectie, klikt u op **configureren Asana** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7d5ab-164">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7d5ab-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Asana configuratie](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="7d5ab-166">In een ander browservenster, aanmelding tooyour Asana toepassing.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="7d5ab-167">tooconfigure SSO in Asana, toegang Hallo werkruimte-instellingen door te klikken op Hallo de naam van de werkruimte op Hallo rechtsboven welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="7d5ab-168">Klik vervolgens op  **\<naam van uw werkruimte\> instellingen**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Asana SSO-instellingen](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="7d5ab-170">Op Hallo **organisatie-instellingen** venster, klikt u op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="7d5ab-171">Klik vervolgens op **leden moeten zich aanmelden via SAML** tooenable Hallo SSO-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="7d5ab-172">Hallo Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-172">hello perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding, organisatie-instellingen configureren](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="7d5ab-174">a.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-174">a.</span></span> <span data-ttu-id="7d5ab-175">In Hallo **aanmelden pagina-URL** textbox plakken Hallo **SAML Single Sign-On Service-URL**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="7d5ab-176">b.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-176">b.</span></span> <span data-ttu-id="7d5ab-177">Klik met de rechtermuisknop op Hallo-certificaat gedownload vanuit Azure-portal, open vervolgens Hallo certificaatbestand in Kladblok of uw voorkeur teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="7d5ab-178">Kopiëren Hallo inhoud tussen Hallo beginnen en end certificaattitel Hallo en plak deze in Hallo **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="7d5ab-179">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-179">Click **Save**.</span></span> <span data-ttu-id="7d5ab-180">Ga te[Asana-handleiding voor het instellen van eenmalige aanmelding](https://asana.com/guide/help/premium/authentication#gl-saml) als u meer hulp nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="7d5ab-181">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7d5ab-182">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7d5ab-183">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d5ab-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7d5ab-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7d5ab-184">Create an Azure AD test user</span></span>

<span data-ttu-id="7d5ab-185">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="7d5ab-187">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7d5ab-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d5ab-188">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d5ab-190">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d5ab-192">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d5ab-194">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d5ab-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d5ab-196">a.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-196">a.</span></span> <span data-ttu-id="7d5ab-197">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d5ab-198">b.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-198">b.</span></span> <span data-ttu-id="7d5ab-199">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d5ab-200">c.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-200">c.</span></span> <span data-ttu-id="7d5ab-201">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7d5ab-202">d.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-202">d.</span></span> <span data-ttu-id="7d5ab-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="7d5ab-204">Een testgebruiker Asana maken</span><span class="sxs-lookup"><span data-stu-id="7d5ab-204">Create an Asana test user</span></span>

<span data-ttu-id="7d5ab-205">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Asana maken.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="7d5ab-206">Op **Asana**, gaat u toohello **Teams** sectie in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="7d5ab-207">Klik op Hallo plus knop aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-207">Click hello plus sign button.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="7d5ab-209">Typ Hallo e britta.simon@contoso.com in het tekstvak Hallo en selecteer vervolgens **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="7d5ab-210">Klik op **uitnodiging verzenden**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-210">Click **Send Invite**.</span></span> <span data-ttu-id="7d5ab-211">Hallo nieuwe gebruiker ontvangt een e-mailbericht in haar e-mailaccount.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="7d5ab-212">Ze toocreate nodig hebt en Hallo account valideren.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7d5ab-213">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d5ab-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7d5ab-214">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAsana toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Hallo-gebruikersrollen toewijzen][200]

<span data-ttu-id="7d5ab-216">**tooassign Britta Simon tooAsana, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7d5ab-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d5ab-217">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7d5ab-219">Selecteer in de lijst met de toepassingen van Hallo **Asana**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-219">In hello applications list, select **Asana**.</span></span>

    ![Hallo Asana koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="7d5ab-221">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="7d5ab-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-223">Click **Add** button.</span></span> <span data-ttu-id="7d5ab-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="7d5ab-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7d5ab-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d5ab-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7d5ab-229">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7d5ab-229">Test single sign-on</span></span>

<span data-ttu-id="7d5ab-230">Hallo-doel van deze sectie is tootest uw Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="7d5ab-231">Ga tooAsana aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-231">Go tooAsana login page.</span></span> <span data-ttu-id="7d5ab-232">Invoegen in Hallo e-mailadres tekstvak Hallo e-mailadres britta.simon@contoso.com. Hallo wachtwoordtekstvak laat in leeg en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="7d5ab-233">U zult omgeleid tooAzure AD-aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="7d5ab-234">Voer uw Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="7d5ab-235">U bent nu aangemeld op Asana.</span><span class="sxs-lookup"><span data-stu-id="7d5ab-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d5ab-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7d5ab-236">Additional resources</span></span>

* [<span data-ttu-id="7d5ab-237">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d5ab-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d5ab-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7d5ab-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
