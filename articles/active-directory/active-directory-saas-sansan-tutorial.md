---
title: 'Zelfstudie: Azure Active Directory-integratie met Sansan | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Sansan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: f58cc613a2e3a240e555b61a34db4155eb9dff71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="8dcd4-103">Zelfstudie: Azure Active Directory-integratie met Sansan</span><span class="sxs-lookup"><span data-stu-id="8dcd4-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="8dcd4-104">In deze zelfstudie leert u hoe toointegrate Sansan met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8dcd4-104">In this tutorial, you learn how toointegrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8dcd4-105">Sansan integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-105">Integrating Sansan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8dcd4-106">U kunt beheren in Azure AD die tooSansan toegang heeft</span><span class="sxs-lookup"><span data-stu-id="8dcd4-106">You can control in Azure AD who has access tooSansan</span></span>
- <span data-ttu-id="8dcd4-107">U kunt uw gebruikers tooautomatically get aangemelde tooSansan (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="8dcd4-107">You can enable your users tooautomatically get signed-on tooSansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8dcd4-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8dcd4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8dcd4-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8dcd4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dcd4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8dcd4-110">Prerequisites</span></span>

<span data-ttu-id="8dcd4-111">Azure AD-integratie met Sansan tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-111">tooconfigure Azure AD integration with Sansan, you need hello following items:</span></span>

- <span data-ttu-id="8dcd4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8dcd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8dcd4-113">Een Sansan eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8dcd4-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8dcd4-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8dcd4-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8dcd4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8dcd4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8dcd4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8dcd4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8dcd4-118">Scenario description</span></span>
<span data-ttu-id="8dcd4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8dcd4-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8dcd4-121">Het toevoegen van Sansan van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8dcd4-121">Adding Sansan from hello gallery</span></span>
2. <span data-ttu-id="8dcd4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8dcd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-hello-gallery"></a><span data-ttu-id="8dcd4-123">Het toevoegen van Sansan van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8dcd4-123">Adding Sansan from hello gallery</span></span>
<span data-ttu-id="8dcd4-124">tooconfigure hello integratie van Sansan in Azure AD, moet u tooadd Sansan uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-124">tooconfigure hello integration of Sansan into Azure AD, you need tooadd Sansan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8dcd4-125">**tooadd Sansan via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8dcd4-125">**tooadd Sansan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dcd4-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8dcd4-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8dcd4-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8dcd4-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8dcd4-133">Typ in het zoekvak Hallo **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-133">In hello search box, type **Sansan**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="8dcd4-135">Selecteer in het deelvenster resultaten hello, **Sansan**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-135">In hello results panel, select **Sansan**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8dcd4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8dcd4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8dcd4-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Sansan op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8dcd4-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Sansan is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sansan is tooa user in Azure AD.</span></span> <span data-ttu-id="8dcd4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Sansan toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-140">In other words, a link relationship between an Azure AD user and hello related user in Sansan needs toobe established.</span></span>

<span data-ttu-id="8dcd4-141">Wijs in Sansan, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-141">In Sansan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8dcd4-142">tooconfigure en eenmalige aanmelding Azure AD-test met Sansan, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-142">tooconfigure and test Azure AD single sign-on with Sansan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8dcd4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8dcd4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8dcd4-145">**[Maken van een testgebruiker Sansan](#creating-a-sansan-test-user)**  -toohave een equivalent van Britta Simon in Sansan die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - toohave a counterpart of Britta Simon in Sansan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8dcd4-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8dcd4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8dcd4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8dcd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8dcd4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Sansan configureren.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="8dcd4-150">**Azure AD tooconfigure eenmalige aanmelding met Sansan, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8dcd4-150">**tooconfigure Azure AD single sign-on with Sansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dcd4-151">In de Azure-portal op Hallo Hallo **Sansan** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-151">In hello Azure portal, on hello **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8dcd4-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="8dcd4-155">Op Hallo **Sansan domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-155">On hello **Sansan Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="8dcd4-157">a.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-157">a.</span></span> <span data-ttu-id="8dcd4-158">In Hallo **aanmeldings-URL** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | <span data-ttu-id="8dcd4-159">Omgeving</span><span class="sxs-lookup"><span data-stu-id="8dcd4-159">Environment</span></span> | <span data-ttu-id="8dcd4-160">URL</span><span class="sxs-lookup"><span data-stu-id="8dcd4-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="8dcd4-161">PC web</span><span class="sxs-lookup"><span data-stu-id="8dcd4-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="8dcd4-162">Systeemeigen mobiele app</span><span class="sxs-lookup"><span data-stu-id="8dcd4-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="8dcd4-163">Mobiele-browserinstellingen</span><span class="sxs-lookup"><span data-stu-id="8dcd4-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="8dcd4-164">b.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-164">b.</span></span> <span data-ttu-id="8dcd4-165">In Hallo **id** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-165">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="8dcd4-166">Omgeving</span><span class="sxs-lookup"><span data-stu-id="8dcd4-166">Environment</span></span>             | <span data-ttu-id="8dcd4-167">URL</span><span class="sxs-lookup"><span data-stu-id="8dcd4-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="8dcd4-168">PC web</span><span class="sxs-lookup"><span data-stu-id="8dcd4-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="8dcd4-169">Systeemeigen mobiele app</span><span class="sxs-lookup"><span data-stu-id="8dcd4-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="8dcd4-170">Mobiele-browserinstellingen</span><span class="sxs-lookup"><span data-stu-id="8dcd4-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="8dcd4-171">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-171">These values are not real.</span></span> <span data-ttu-id="8dcd4-172">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-172">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8dcd4-173">Neem contact op met [Sansan Client ondersteuningsteam](https://www.sansan.com/form/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) tooget these values.</span></span> 

4. <span data-ttu-id="8dcd4-174">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-174">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="8dcd4-176">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-176">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8dcd4-178">Op Hallo **Sansan configuratie** sectie, klikt u op **configureren Sansan** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-178">On hello **Sansan Configuration** section, click **Configure Sansan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8dcd4-179">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="8dcd4-179">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="8dcd4-181">tooconfigure eenmalige aanmelding op **Sansan** zijde, moet u toosend Hallo gedownload **certificaat**, **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** te[Sansan ondersteuningsteam](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="8dcd4-181">tooconfigure single sign-on on **Sansan** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="8dcd4-182">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-182">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="8dcd4-183">PC browserinstelling werken ook voor mobiele Apps en mobiele browser samen met PC web.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="8dcd4-184">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8dcd4-185">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8dcd4-186">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8dcd4-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8dcd4-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8dcd4-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="8dcd4-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8dcd4-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8dcd4-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dcd4-191">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8dcd4-193">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8dcd4-195">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8dcd4-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8dcd4-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8dcd4-199">a.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-199">a.</span></span> <span data-ttu-id="8dcd4-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8dcd4-201">b.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-201">b.</span></span> <span data-ttu-id="8dcd4-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8dcd4-203">c.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-203">c.</span></span> <span data-ttu-id="8dcd4-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8dcd4-205">d.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-205">d.</span></span> <span data-ttu-id="8dcd4-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="8dcd4-207">Een testgebruiker Sansan maken</span><span class="sxs-lookup"><span data-stu-id="8dcd4-207">Creating a Sansan test user</span></span>

<span data-ttu-id="8dcd4-208">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in SanSan maken.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="8dcd4-209">SanSan toepassing moet Hallo gebruiker toobe ingericht in de toepassing hello voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-209">SanSan application needs hello user toobe provisioned in hello application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="8dcd4-210">Als u handmatig een gebruiker toocreate moet of batch-gebruikers, moet u toocontact hello [Sansan ondersteuningsteam](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="8dcd4-210">If you need toocreate a user manually or batch of users, you need toocontact hello [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8dcd4-211">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dcd4-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8dcd4-212">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSansan toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSansan.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8dcd4-214">**tooassign Britta Simon tooSansan, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8dcd4-214">**tooassign Britta Simon tooSansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dcd4-215">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8dcd4-217">Selecteer in de lijst met de toepassingen van Hallo **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-217">In hello applications list, select **Sansan**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="8dcd4-219">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8dcd4-221">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-221">Click **Add** button.</span></span> <span data-ttu-id="8dcd4-222">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8dcd4-224">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8dcd4-225">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8dcd4-226">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8dcd4-227">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8dcd4-227">Testing single sign-on</span></span>

<span data-ttu-id="8dcd4-228">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8dcd4-229">Als u op Hallo Sansan tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Sansan toepassing.</span><span class="sxs-lookup"><span data-stu-id="8dcd4-229">When you click hello Sansan tile in hello Access Panel, you should get automatically signed-on tooyour Sansan application.</span></span>
<span data-ttu-id="8dcd4-230">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dcd4-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8dcd4-231">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8dcd4-231">Additional resources</span></span>

* [<span data-ttu-id="8dcd4-232">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dcd4-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8dcd4-233">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8dcd4-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

