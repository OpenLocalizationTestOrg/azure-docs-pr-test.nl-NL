---
title: 'Zelfstudie: Azure Active Directory-integratie met Kronos | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kronos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="ba4bc-103">Zelfstudie: Azure Active Directory-integratie met Kronos</span><span class="sxs-lookup"><span data-stu-id="ba4bc-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="ba4bc-104">In deze zelfstudie leert u hoe toointegrate Kronos met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba4bc-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba4bc-105">Kronos integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ba4bc-106">U kunt beheren in Azure AD die tooKronos toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ba4bc-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="ba4bc-107">U kunt uw gebruikers tooautomatically get aangemelde tooKronos (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ba4bc-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba4bc-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ba4bc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ba4bc-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba4bc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba4bc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ba4bc-110">Prerequisites</span></span>

<span data-ttu-id="ba4bc-111">Azure AD-integratie met Kronos tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="ba4bc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ba4bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba4bc-113">Een **Kronos medewerkers centrale** SSO abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="ba4bc-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba4bc-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba4bc-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba4bc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba4bc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba4bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba4bc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ba4bc-118">Scenario description</span></span>
<span data-ttu-id="ba4bc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba4bc-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba4bc-121">Het toevoegen van Kronos van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ba4bc-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="ba4bc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ba4bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="ba4bc-123">Het toevoegen van Kronos van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ba4bc-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="ba4bc-124">tooconfigure hello integratie van Kronos in Azure AD, moet u tooadd Kronos uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ba4bc-125">**tooadd Kronos via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ba4bc-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba4bc-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba4bc-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ba4bc-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ba4bc-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ba4bc-133">Typ in het zoekvak Hallo **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-133">In hello search box, type **Kronos**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="ba4bc-135">Selecteer in het deelvenster resultaten hello, **Kronos**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba4bc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ba4bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba4bc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Kronos op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ba4bc-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ba4bc-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kronos is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="ba4bc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kronos toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="ba4bc-141">Wijs in Kronos, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ba4bc-142">tooconfigure en eenmalige aanmelding Azure AD-test met Kronos, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ba4bc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ba4bc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba4bc-145">**[Maken van een testgebruiker Kronos](#creating-a-kronos-test-user)**  -toohave een equivalent van Britta Simon in Kronos die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba4bc-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba4bc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba4bc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ba4bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba4bc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Kronos configureren.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="ba4bc-150">**Azure AD tooconfigure eenmalige aanmelding met Kronos, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ba4bc-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba4bc-151">In de Azure-portal op Hallo Hallo **Kronos** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ba4bc-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="ba4bc-155">Op Hallo **Kronos domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="ba4bc-157">a.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-157">a.</span></span> <span data-ttu-id="ba4bc-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="ba4bc-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="ba4bc-159">b.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-159">b.</span></span> <span data-ttu-id="ba4bc-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="ba4bc-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ba4bc-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-161">These values are not real.</span></span> <span data-ttu-id="ba4bc-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ba4bc-163">Neem contact op met [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="ba4bc-164">Uw toepassing Kronos verwacht Hallo SAML asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ba4bc-165">Werken met [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) eerste tooidentify Hallo juiste gebruikers-id, die in de toepassing hello is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="ba4bc-166">Neem even ook Hallo hulp bij het Hallo-kenmerk, dat hij of zij wil toouse voor deze toewijzing.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="ba4bc-167">Microsoft raadt u Hallo **'NameIdentifier'** kenmerk als gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="ba4bc-168">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerken'** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="ba4bc-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="ba4bc-170">Hier wordt de Hallo hebt toegewezen **gebruikers-id (nameid)** met **ExtractMailPrefix()** functie van **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="ba4bc-171">Dit geeft voorvoegsel op Hallo van e-mailadres van Hallo-gebruiker die is Hallo unieke gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="ba4bc-172">Dit wordt toohello Kronos toepassing in elke geslaagde reactie verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="ba4bc-174">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="ba4bc-175">a.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-175">a.</span></span> <span data-ttu-id="ba4bc-176">Selecteer in de vervolgkeuzelijst Hallo gebruikers-id, **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="ba4bc-177">b.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-177">b.</span></span> <span data-ttu-id="ba4bc-178">In Hallo **Mail** vervolgkeuzelijst, selecteer **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="ba4bc-179">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="ba4bc-181">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-181">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ba4bc-183">tooconfigure eenmalige aanmelding op **Kronos** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="ba4bc-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="ba4bc-184">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ba4bc-185">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ba4bc-186">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba4bc-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba4bc-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ba4bc-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba4bc-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ba4bc-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ba4bc-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba4bc-191">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba4bc-193">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba4bc-195">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba4bc-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ba4bc-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba4bc-199">a.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-199">a.</span></span> <span data-ttu-id="ba4bc-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba4bc-201">b.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-201">b.</span></span> <span data-ttu-id="ba4bc-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba4bc-203">c.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-203">c.</span></span> <span data-ttu-id="ba4bc-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ba4bc-205">d.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-205">d.</span></span> <span data-ttu-id="ba4bc-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="ba4bc-207">Een testgebruiker Kronos maken</span><span class="sxs-lookup"><span data-stu-id="ba4bc-207">Creating a Kronos test user</span></span>

<span data-ttu-id="ba4bc-208">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Kronos maken.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="ba4bc-209">Kronos toepassing moet alle Hallo gebruikers toobe ingericht in de toepassing hello voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="ba4bc-210">Werken met Hallo [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) tooprovision deze gebruikers in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ba4bc-211">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba4bc-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ba4bc-212">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKronos toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ba4bc-214">**tooassign Britta Simon tooKronos, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ba4bc-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba4bc-215">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ba4bc-217">Selecteer in de lijst met de toepassingen van Hallo **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-217">In hello applications list, select **Kronos**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="ba4bc-219">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ba4bc-221">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-221">Click **Add** button.</span></span> <span data-ttu-id="ba4bc-222">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ba4bc-224">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ba4bc-225">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba4bc-226">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba4bc-227">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ba4bc-227">Testing single sign-on</span></span>

<span data-ttu-id="ba4bc-228">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ba4bc-229">Als u op Hallo Kronos-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Kronos toepassing.</span><span class="sxs-lookup"><span data-stu-id="ba4bc-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba4bc-230">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ba4bc-230">Additional resources</span></span>

* [<span data-ttu-id="ba4bc-231">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba4bc-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba4bc-232">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ba4bc-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

