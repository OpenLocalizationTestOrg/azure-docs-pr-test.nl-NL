---
title: 'Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Splunk Enterprise en Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 848e0485131321479f2375501b330c798627e7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="429f9-103">Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="429f9-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="429f9-104">In deze zelfstudie leert u hoe toointegrate Splunk Enterprise en Splunk Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="429f9-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="429f9-105">Splunk Enterprise en Splunk Cloud integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="429f9-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="429f9-106">U kunt beheren in Azure AD die toegang heeft tooSplunk Enterprise en Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="429f9-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="429f9-107">U kunt uw gebruikers tooautomatically get aangemelde tooSplunk Enterprise en Splunk Cloud (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="429f9-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="429f9-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="429f9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="429f9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="429f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="429f9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="429f9-110">Prerequisites</span></span>

<span data-ttu-id="429f9-111">Azure AD-integratie met Splunk Enterprise en Splunk Cloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="429f9-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="429f9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="429f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="429f9-113">Een Splunk Enterprise en Splunk Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="429f9-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="429f9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="429f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="429f9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="429f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="429f9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="429f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="429f9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="429f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="429f9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="429f9-118">Scenario description</span></span>
<span data-ttu-id="429f9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="429f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="429f9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="429f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="429f9-121">Splunk Enterprise en Splunk Cloud toe te voegen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="429f9-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="429f9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="429f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="429f9-123">Splunk Enterprise en Splunk Cloud toe te voegen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="429f9-123">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="429f9-124">tooconfigure hello integratie van Splunk Enterprise en Splunk Cloud met Azure AD, moet u tooadd Splunk Enterprise en Splunk Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="429f9-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="429f9-125">**tooadd Splunk Enterprise en Splunk Cloud uit de galerie hello, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="429f9-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="429f9-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="429f9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="429f9-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="429f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="429f9-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="429f9-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="429f9-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="429f9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="429f9-133">Typ in het zoekvak Hallo **Splunk Enterprise en Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="429f9-133">In hello search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="429f9-135">Selecteer in het deelvenster resultaten hello, **Splunk Enterprise en Splunk Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="429f9-135">In hello results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="429f9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="429f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="429f9-138">In deze sectie maakt u configureren en testen Azure AD eenmalige aanmelding met Splunk voor ondernemingen en Splunk Cloud op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="429f9-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="429f9-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Splunk Enterprise en Splunk Cloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="429f9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="429f9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Splunk Enterprise en Splunk Cloud toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="429f9-140">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="429f9-141">In Splunk Enterprise en Splunk Cloud toewijzen Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="429f9-141">In Splunk Enterprise and Splunk Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="429f9-142">tooconfigure en eenmalige aanmelding Azure AD-test met Splunk Enterprise en Splunk Cloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="429f9-142">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="429f9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="429f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="429f9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="429f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="429f9-145">**[Maken van een testgebruiker Splunk Enterprise en Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave een equivalent van Britta Simon in de onderneming Splunk en Splunk Cloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="429f9-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="429f9-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="429f9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="429f9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="429f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="429f9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="429f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="429f9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="429f9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="429f9-150">**tooconfigure eenmalige aanmelding Azure AD met Splunk Enterprise en Splunk Cloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="429f9-150">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="429f9-151">In de Azure-portal op Hallo Hallo **Splunk Enterprise en Splunk Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="429f9-151">In hello Azure portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="429f9-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="429f9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="429f9-155">Op Hallo **Splunk Enterprise en Splunk Cloud-domein en URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="429f9-155">On hello **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="429f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="429f9-157">a.</span></span> <span data-ttu-id="429f9-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="429f9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="429f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="429f9-159">b.</span></span> <span data-ttu-id="429f9-160">In Hallo **id** textbox type Hallo-URL van uw Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="429f9-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>

    <span data-ttu-id="429f9-161">c.</span><span class="sxs-lookup"><span data-stu-id="429f9-161">c.</span></span> <span data-ttu-id="429f9-162">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="429f9-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="429f9-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="429f9-163">These values are not real.</span></span> <span data-ttu-id="429f9-164">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="429f9-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="429f9-165">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="429f9-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="429f9-166">Neem contact op met [Splunk Enterprise- en Cloud-Client Splunk ondersteuningsteam](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="429f9-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget these values.</span></span> 

4. <span data-ttu-id="429f9-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="429f9-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="429f9-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="429f9-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="429f9-171">tooconfigure eenmalige aanmelding op **Splunk Enterprise en Splunk Cloud** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Splunk Enterprise en Splunk Cloud ondersteuningsteam](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="429f9-171">tooconfigure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need toosend hello downloaded **Metadata XML** too[Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="429f9-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="429f9-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="429f9-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="429f9-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="429f9-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="429f9-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="429f9-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="429f9-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="429f9-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="429f9-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="429f9-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="429f9-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="429f9-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="429f9-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="429f9-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="429f9-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="429f9-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="429f9-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="429f9-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="429f9-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="429f9-187">a.</span><span class="sxs-lookup"><span data-stu-id="429f9-187">a.</span></span> <span data-ttu-id="429f9-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="429f9-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="429f9-189">b.</span><span class="sxs-lookup"><span data-stu-id="429f9-189">b.</span></span> <span data-ttu-id="429f9-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="429f9-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="429f9-191">c.</span><span class="sxs-lookup"><span data-stu-id="429f9-191">c.</span></span> <span data-ttu-id="429f9-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="429f9-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="429f9-193">d.</span><span class="sxs-lookup"><span data-stu-id="429f9-193">d.</span></span> <span data-ttu-id="429f9-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="429f9-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="429f9-195">Een testgebruiker Splunk Enterprise en Splunk Cloud maken</span><span class="sxs-lookup"><span data-stu-id="429f9-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="429f9-196">In deze sectie maakt u een gebruiker met de naam Britta Simon in de onderneming Splunk en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="429f9-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="429f9-197">Werken met [Splunk Enterprise en Splunk Cloud ondersteuningsteam](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd Hallo gebruikers in Hallo Splunk Enterprise en Splunk Cloud-platform.</span><span class="sxs-lookup"><span data-stu-id="429f9-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="429f9-198">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="429f9-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="429f9-199">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSplunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="429f9-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="429f9-201">**tooassign Britta Simon tooSplunk Enterprise en Splunk Cloud uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="429f9-201">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="429f9-202">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="429f9-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="429f9-204">Selecteer in de lijst met de toepassingen van Hallo **Splunk Enterprise en Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="429f9-204">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="429f9-206">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="429f9-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="429f9-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="429f9-208">Click **Add** button.</span></span> <span data-ttu-id="429f9-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="429f9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="429f9-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="429f9-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="429f9-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="429f9-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="429f9-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="429f9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="429f9-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="429f9-214">Testing single sign-on</span></span>

<span data-ttu-id="429f9-215">In deze sectie kunt u uw Azure AD-SSOonfiguration Hallo Toegangsvenster met testen.</span><span class="sxs-lookup"><span data-stu-id="429f9-215">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="429f9-216">Wanneer u hello Splunk Enterprise- en Splunk Cloud-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Splunk Enterprise en Splunk Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="429f9-216">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="429f9-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="429f9-217">Additional resources</span></span>

* [<span data-ttu-id="429f9-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="429f9-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="429f9-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="429f9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

