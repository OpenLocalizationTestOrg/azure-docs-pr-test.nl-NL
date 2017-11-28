---
title: 'Zelfstudie: Azure Active Directory-integratie met Neota logica Studio | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Neota logica Studio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="f83d0-103">Zelfstudie: Azure Active Directory-integratie met Neota logica Studio</span><span class="sxs-lookup"><span data-stu-id="f83d0-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="f83d0-104">In deze zelfstudie leert u hoe toointegrate Neota logica Studio met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f83d0-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f83d0-105">Neota logica Studio integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f83d0-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f83d0-106">U kunt beheren in Azure AD wie toegang tot tooNeota logica Studio heeft</span><span class="sxs-lookup"><span data-stu-id="f83d0-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="f83d0-107">U kunt uw gebruikers tooautomatically get aangemelde tooNeota logica Studio (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f83d0-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f83d0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f83d0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f83d0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="f83d0-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="f83d0-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f83d0-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f83d0-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f83d0-111">Prerequisites</span></span>

<span data-ttu-id="f83d0-112">Azure AD-integratie met Neota logica Studio tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f83d0-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="f83d0-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f83d0-113">An Azure AD subscription</span></span>
- <span data-ttu-id="f83d0-114">Een Neota logica Studio eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f83d0-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f83d0-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f83d0-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f83d0-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f83d0-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f83d0-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f83d0-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f83d0-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f83d0-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f83d0-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f83d0-119">Scenario description</span></span>

<span data-ttu-id="f83d0-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f83d0-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f83d0-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f83d0-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f83d0-122">Het toevoegen van Neota logica Studio van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f83d0-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="f83d0-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f83d0-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="f83d0-124">Het toevoegen van Neota logica Studio van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f83d0-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="f83d0-125">tooconfigure hello integratie van Neota logica Studio in Azure AD, moet u tooadd Neota logica Studio uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f83d0-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f83d0-126">**tooadd Neota logica Studio via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83d0-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83d0-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f83d0-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f83d0-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f83d0-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f83d0-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83d0-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f83d0-134">Typ in het zoekvak Hallo **Neota logica Studio**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="f83d0-136">Selecteer in het deelvenster resultaten hello, **Neota logica Studio**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f83d0-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f83d0-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f83d0-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="f83d0-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Neota logica Studio op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f83d0-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f83d0-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Neota logica Studio is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f83d0-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="f83d0-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Neota logica Studio toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f83d0-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="f83d0-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Neota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="f83d0-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="f83d0-143">tooconfigure en test eenmalige aanmelding Azure AD met Neota logica Studio, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f83d0-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f83d0-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f83d0-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f83d0-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f83d0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f83d0-146">**[Maken van een testgebruiker Neota logica Studio](#creating-a-neota-logic-studio-test-user)**  -toohave een equivalent van Britta Simon in Neota logica Studio die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f83d0-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f83d0-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f83d0-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f83d0-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f83d0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f83d0-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f83d0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f83d0-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Neota logica Studio configureren.</span><span class="sxs-lookup"><span data-stu-id="f83d0-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="f83d0-151">**tooconfigure eenmalige aanmelding Azure AD met Neota logica Studio, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83d0-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83d0-152">In de Azure-portal op Hallo Hallo **Neota logica Studio** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f83d0-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f83d0-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="f83d0-156">Op Hallo **Neota logica Studio domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f83d0-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="f83d0-158">a.</span><span class="sxs-lookup"><span data-stu-id="f83d0-158">a.</span></span> <span data-ttu-id="f83d0-159">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="f83d0-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="f83d0-160">b.</span><span class="sxs-lookup"><span data-stu-id="f83d0-160">b.</span></span> <span data-ttu-id="f83d0-161">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="f83d0-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f83d0-162">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="f83d0-162">These values are not hello real.</span></span> <span data-ttu-id="f83d0-163">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL & -id.</span><span class="sxs-lookup"><span data-stu-id="f83d0-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="f83d0-164">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="f83d0-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="f83d0-165">Neem contact op met [Neota logica Studio Client ondersteuningsteam](https://www.neotalogic.com/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f83d0-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="f83d0-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f83d0-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="f83d0-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f83d0-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f83d0-170">tooget SSO is geconfigureerd voor uw toepassing, neem contact op met [Neota logica Studio ondersteuning](https://www.neotalogic.com/contact-us/) team en bieden ze gedownload met **Metadata XML** bestand.</span><span class="sxs-lookup"><span data-stu-id="f83d0-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="f83d0-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f83d0-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f83d0-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f83d0-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f83d0-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f83d0-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f83d0-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f83d0-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="f83d0-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f83d0-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f83d0-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83d0-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83d0-178">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f83d0-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f83d0-180">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f83d0-182">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f83d0-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f83d0-184">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f83d0-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f83d0-186">a.</span><span class="sxs-lookup"><span data-stu-id="f83d0-186">a.</span></span> <span data-ttu-id="f83d0-187">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f83d0-188">b.</span><span class="sxs-lookup"><span data-stu-id="f83d0-188">b.</span></span> <span data-ttu-id="f83d0-189">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f83d0-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f83d0-190">c.</span><span class="sxs-lookup"><span data-stu-id="f83d0-190">c.</span></span> <span data-ttu-id="f83d0-191">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f83d0-192">d.</span><span class="sxs-lookup"><span data-stu-id="f83d0-192">d.</span></span> <span data-ttu-id="f83d0-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="f83d0-194">Een testgebruiker Neota logica Studio maken</span><span class="sxs-lookup"><span data-stu-id="f83d0-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="f83d0-195">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Neota logica Studio maken.</span><span class="sxs-lookup"><span data-stu-id="f83d0-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="f83d0-196">werken met [Neota logica Studio Client ondersteuningsteam](https://www.neotalogic.com/contact-us/) Hallo gebruikers toevoegen in Hallo Neota logica Studio platform.</span><span class="sxs-lookup"><span data-stu-id="f83d0-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="f83d0-197">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f83d0-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f83d0-198">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f83d0-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f83d0-199">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooNeota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="f83d0-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f83d0-201">**tooassign Britta Simon tooNeota logica Studio, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f83d0-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83d0-202">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f83d0-204">Selecteer in de lijst met de toepassingen van Hallo **Neota logica Studio**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="f83d0-206">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f83d0-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f83d0-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f83d0-208">Click **Add** button.</span></span> <span data-ttu-id="f83d0-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83d0-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f83d0-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f83d0-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f83d0-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83d0-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f83d0-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f83d0-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f83d0-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f83d0-214">Testing single sign-on</span></span>

<span data-ttu-id="f83d0-215">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f83d0-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f83d0-216">Klik op Hallo Neota logica Studio tegel in het deelvenster toegang hello, kunt u zich omgeleide tooOrganization aanmelding pagina.</span><span class="sxs-lookup"><span data-stu-id="f83d0-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="f83d0-217">U zult na geslaagde aanmelding aangemelde tooyour Neota logica Studio-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f83d0-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="f83d0-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f83d0-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="f83d0-219">Zie voor meer informatie over Hallo Toegangspaneel [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f83d0-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f83d0-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f83d0-220">Additional resources</span></span>

* [<span data-ttu-id="f83d0-221">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f83d0-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f83d0-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f83d0-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

