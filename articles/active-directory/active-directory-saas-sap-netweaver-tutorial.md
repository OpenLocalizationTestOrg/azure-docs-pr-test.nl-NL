---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP NetWeaver | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP NetWeaver.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 69008734864e1e258a0c2ec872e51aa331491fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="6b05c-103">Zelfstudie: Azure Active Directory-integratie met SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="6b05c-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="6b05c-104">In deze zelfstudie leert u hoe toointegrate SAP NetWeaver met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b05c-104">In this tutorial, you learn how toointegrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b05c-105">SAP NetWeaver integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6b05c-105">Integrating SAP NetWeaver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6b05c-106">U kunt beheren in Azure AD wie toegang tot tooSAP NetWeaver heeft</span><span class="sxs-lookup"><span data-stu-id="6b05c-106">You can control in Azure AD who has access tooSAP NetWeaver</span></span>
- <span data-ttu-id="6b05c-107">U kunt uw gebruikers tooautomatically get aangemelde tooSAP NetWeaver (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6b05c-107">You can enable your users tooautomatically get signed-on tooSAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b05c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6b05c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6b05c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b05c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6b05c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6b05c-110">Prerequisites</span></span>

<span data-ttu-id="6b05c-111">Azure AD-integratie met SAP NetWeaver tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6b05c-111">tooconfigure Azure AD integration with SAP NetWeaver, you need hello following items:</span></span>

- <span data-ttu-id="6b05c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6b05c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b05c-113">Een SAP NetWeaver eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6b05c-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b05c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b05c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b05c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6b05c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b05c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6b05c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b05c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b05c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b05c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6b05c-118">Scenario description</span></span>
<span data-ttu-id="6b05c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6b05c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b05c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6b05c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b05c-121">SAP NetWeaver uit Hallo galerie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="6b05c-121">Adding SAP NetWeaver from hello gallery</span></span>
2. <span data-ttu-id="6b05c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b05c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-hello-gallery"></a><span data-ttu-id="6b05c-123">SAP NetWeaver uit Hallo galerie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="6b05c-123">Adding SAP NetWeaver from hello gallery</span></span>
<span data-ttu-id="6b05c-124">tooconfigure hello integratie van SAP NetWeaver in Azure AD, moet u tooadd SAP NetWeaver uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6b05c-124">tooconfigure hello integration of SAP NetWeaver into Azure AD, you need tooadd SAP NetWeaver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6b05c-125">**SAP NetWeaver via Hallo gallery tooadd uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b05c-125">**tooadd SAP NetWeaver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b05c-126">In Hallo  **[Azure Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b05c-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6b05c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6b05c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6b05c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b05c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6b05c-133">Typ in het zoekvak Hallo **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-133">In hello search box, type **SAP NetWeaver**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="6b05c-135">Selecteer in het deelvenster resultaten hello, **SAP NetWeaver**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b05c-135">In hello results panel, select **SAP NetWeaver**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b05c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b05c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b05c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SAP NetWeaver op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6b05c-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6b05c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SAP NetWeaver is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b05c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP NetWeaver is tooa user in Azure AD.</span></span> <span data-ttu-id="6b05c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SAP NetWeaver toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6b05c-140">In other words, a link relationship between an Azure AD user and hello related user in SAP NetWeaver needs toobe established.</span></span>

<span data-ttu-id="6b05c-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="6b05c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="6b05c-142">tooconfigure en eenmalige aanmelding Azure AD-test met SAP NetWeaver, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b05c-142">tooconfigure and test Azure AD single sign-on with SAP NetWeaver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6b05c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6b05c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6b05c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b05c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b05c-145">**[Maken van een testgebruiker SAP NetWeaver](#creating-an-sap-netweaver-test-user)**  -toohave een equivalent van Britta Simon in SAP NetWeaver die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6b05c-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - toohave a counterpart of Britta Simon in SAP NetWeaver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b05c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6b05c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b05c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6b05c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b05c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6b05c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b05c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing SAP NetWeaver configureren.</span><span class="sxs-lookup"><span data-stu-id="6b05c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="6b05c-150">**Voer tooconfigure Azure AD eenmalige aanmelding met SAP NetWeaver Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b05c-150">**tooconfigure Azure AD single sign-on with SAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b05c-151">In de Azure-portal op Hallo Hallo **SAP NetWeaver** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-151">In hello Azure portal, on hello **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6b05c-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6b05c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="6b05c-155">Op Hallo **SAP NetWeaver domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b05c-155">On hello **SAP NetWeaver Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="6b05c-157">a.</span><span class="sxs-lookup"><span data-stu-id="6b05c-157">a.</span></span> <span data-ttu-id="6b05c-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="6b05c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="6b05c-159">b.</span><span class="sxs-lookup"><span data-stu-id="6b05c-159">b.</span></span> <span data-ttu-id="6b05c-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="6b05c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="6b05c-161">c.</span><span class="sxs-lookup"><span data-stu-id="6b05c-161">c.</span></span> <span data-ttu-id="6b05c-162">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="6b05c-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="6b05c-163">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="6b05c-163">These values are not hello real.</span></span> <span data-ttu-id="6b05c-164">Bijwerken van deze waarden met de werkelijke Hallo-id en de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="6b05c-164">Update these values with hello actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="6b05c-165">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="6b05c-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="6b05c-166">Neem contact op met [SAP NetWeaver Client ondersteuningsteam](https://www.sap.com/support.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6b05c-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) tooget these values.</span></span> 

4. <span data-ttu-id="6b05c-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6b05c-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="6b05c-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6b05c-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6b05c-171">Op Hallo **SAP NetWeaver configuratie** sectie, klikt u op **configureren SAP NetWeaver** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6b05c-171">On hello **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6b05c-172">Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6b05c-172">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="6b05c-174">tooconfigure eenmalige aanmelding op **SAP NetWeaver** zijde, moet u toosend Hallo gedownload **Metadata XML** en **SAML entiteit-ID** te[SAP NetWeaver-ondersteuning ](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="6b05c-174">tooconfigure single sign-on on **SAP NetWeaver** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="6b05c-175">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="6b05c-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6b05c-176">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="6b05c-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6b05c-177">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b05c-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b05c-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6b05c-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b05c-179">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6b05c-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6b05c-181">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b05c-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b05c-182">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6b05c-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b05c-184">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b05c-186">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6b05c-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b05c-188">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b05c-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b05c-190">a.</span><span class="sxs-lookup"><span data-stu-id="6b05c-190">a.</span></span> <span data-ttu-id="6b05c-191">In Hallo **naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-191">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="6b05c-192">b.</span><span class="sxs-lookup"><span data-stu-id="6b05c-192">b.</span></span> <span data-ttu-id="6b05c-193">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b05c-193">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="6b05c-194">c.</span><span class="sxs-lookup"><span data-stu-id="6b05c-194">c.</span></span> <span data-ttu-id="6b05c-195">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6b05c-196">d.</span><span class="sxs-lookup"><span data-stu-id="6b05c-196">d.</span></span> <span data-ttu-id="6b05c-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="6b05c-198">Een SAP NetWeaver testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6b05c-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="6b05c-199">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="6b05c-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="6b05c-200">Werken met uw [SAP NetWeaver ondersteuning](https://www.sap.com/support.html) tooadd Hallo gebruikers in Hallo SAP NetWeaver platform.</span><span class="sxs-lookup"><span data-stu-id="6b05c-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) tooadd hello users in hello SAP NetWeaver platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6b05c-201">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b05c-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6b05c-202">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="6b05c-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP NetWeaver.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6b05c-204">**tooassign Britta Simon tooSAP NetWeaver, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6b05c-204">**tooassign Britta Simon tooSAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b05c-205">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6b05c-207">Selecteer in de lijst met de toepassingen van Hallo **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-207">In hello applications list, select **SAP NetWeaver**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="6b05c-209">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6b05c-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6b05c-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6b05c-211">Click **Add** button.</span></span> <span data-ttu-id="6b05c-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b05c-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6b05c-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b05c-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6b05c-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b05c-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b05c-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6b05c-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b05c-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6b05c-217">Testing single sign-on</span></span>

<span data-ttu-id="6b05c-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6b05c-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6b05c-219">Als u op Hallo SAP NetWeaver tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SAP NetWeaver toepassing.</span><span class="sxs-lookup"><span data-stu-id="6b05c-219">When you click hello SAP NetWeaver tile in hello Access Panel, you should get automatically signed-on tooyour SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b05c-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6b05c-220">Additional resources</span></span>

* [<span data-ttu-id="6b05c-221">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b05c-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b05c-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b05c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

