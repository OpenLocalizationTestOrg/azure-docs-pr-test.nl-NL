---
title: 'Zelfstudie: Azure Active Directory-integratie met PerformanceCentre | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PerformanceCentre.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="2ff15-103">Zelfstudie: Azure Active Directory-integratie met PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="2ff15-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="2ff15-104">In deze zelfstudie leert u hoe toointegrate PerformanceCentre met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ff15-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ff15-105">PerformanceCentre integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2ff15-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ff15-106">U kunt beheren in Azure AD die tooPerformanceCentre toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2ff15-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="2ff15-107">U kunt uw gebruikers tooautomatically get aangemelde tooPerformanceCentre (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2ff15-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ff15-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2ff15-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2ff15-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ff15-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ff15-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2ff15-110">Prerequisites</span></span>

<span data-ttu-id="2ff15-111">Azure AD-integratie met PerformanceCentre tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2ff15-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="2ff15-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2ff15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ff15-113">Een PerformanceCentre eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2ff15-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ff15-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2ff15-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ff15-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2ff15-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ff15-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2ff15-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ff15-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ff15-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ff15-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2ff15-118">Scenario description</span></span>
<span data-ttu-id="2ff15-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2ff15-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ff15-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2ff15-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ff15-121">Het toevoegen van PerformanceCentre van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2ff15-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="2ff15-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2ff15-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="2ff15-123">Het toevoegen van PerformanceCentre van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2ff15-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="2ff15-124">tooconfigure hello integratie van PerformanceCentre in Azure AD, moet u tooadd PerformanceCentre uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2ff15-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ff15-125">**tooadd PerformanceCentre via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2ff15-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ff15-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2ff15-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ff15-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ff15-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2ff15-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ff15-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2ff15-133">Typ in het zoekvak Hallo **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="2ff15-135">Selecteer in het deelvenster resultaten hello, **PerformanceCentre**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2ff15-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ff15-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2ff15-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ff15-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met PerformanceCentre op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2ff15-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ff15-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PerformanceCentre is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ff15-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="2ff15-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PerformanceCentre toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2ff15-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="2ff15-141">Wijs in PerformanceCentre, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2ff15-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ff15-142">tooconfigure en eenmalige aanmelding Azure AD-test met PerformanceCentre, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ff15-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ff15-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2ff15-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ff15-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ff15-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ff15-145">**[Maken van een testgebruiker PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave een equivalent van Britta Simon in PerformanceCentre die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2ff15-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ff15-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2ff15-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ff15-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2ff15-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ff15-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2ff15-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ff15-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing PerformanceCentre configureren.</span><span class="sxs-lookup"><span data-stu-id="2ff15-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="2ff15-150">**Azure AD tooconfigure eenmalige aanmelding met PerformanceCentre, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2ff15-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ff15-151">In de Azure-portal op Hallo Hallo **PerformanceCentre** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2ff15-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2ff15-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="2ff15-155">Op Hallo **PerformanceCentre domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ff15-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="2ff15-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ff15-157">a.</span></span> <span data-ttu-id="2ff15-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="2ff15-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="2ff15-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ff15-159">b.</span></span> <span data-ttu-id="2ff15-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="2ff15-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ff15-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2ff15-161">These values are not real.</span></span> <span data-ttu-id="2ff15-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="2ff15-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2ff15-163">Neem contact op met [PerformanceCentre Client ondersteuningsteam](https://www.performancecentre.com/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2ff15-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="2ff15-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2ff15-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="2ff15-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2ff15-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ff15-168">Op Hallo **PerformanceCentre configuratie** sectie, klikt u op **configureren PerformanceCentre** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2ff15-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ff15-169">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2ff15-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="2ff15-171">Eenmalige aanmelding tooyour **PerformanceCentre** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="2ff15-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="2ff15-172">Op het tabblad aan de linkerkant Hallo Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][10]

9. <span data-ttu-id="2ff15-174">Op het tabblad aan de linkerkant Hallo Hallo **overige**, en klik vervolgens op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][11]

10. <span data-ttu-id="2ff15-176">Als **Protocol**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][12]

11. <span data-ttu-id="2ff15-178">Open het metagegevensbestand gedownloade in Kladblok en kopieer Hallo inhoud, plakt u deze in Hallo **identiteit Provider metagegevens** tekstvak en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][13]

12. <span data-ttu-id="2ff15-180">Controleer of dat de waarden voor Hallo Hallo **entiteit basis-URL** en **entiteit-ID URL** juist zijn.</span><span class="sxs-lookup"><span data-stu-id="2ff15-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD voor eenmalige aanmelding][14]

> [!TIP]
> <span data-ttu-id="2ff15-182">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2ff15-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ff15-183">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2ff15-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ff15-184">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ff15-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ff15-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2ff15-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ff15-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2ff15-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2ff15-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2ff15-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ff15-189">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2ff15-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ff15-191">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ff15-193">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2ff15-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ff15-195">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ff15-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ff15-197">a.</span><span class="sxs-lookup"><span data-stu-id="2ff15-197">a.</span></span> <span data-ttu-id="2ff15-198">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ff15-199">b.</span><span class="sxs-lookup"><span data-stu-id="2ff15-199">b.</span></span> <span data-ttu-id="2ff15-200">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2ff15-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ff15-201">c.</span><span class="sxs-lookup"><span data-stu-id="2ff15-201">c.</span></span> <span data-ttu-id="2ff15-202">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2ff15-203">d.</span><span class="sxs-lookup"><span data-stu-id="2ff15-203">d.</span></span> <span data-ttu-id="2ff15-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="2ff15-205">Een testgebruiker PerformanceCentre maken</span><span class="sxs-lookup"><span data-stu-id="2ff15-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="2ff15-206">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in PerformanceCentre van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2ff15-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="2ff15-207">**een gebruiker Britta Simon aangeroepen in PerformanceCentre, toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2ff15-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ff15-208">Meld u op tooyour PerformanceCentre bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2ff15-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="2ff15-209">Klik in het menu aan de linkerkant Hallo Hallo op **Interrelate**, en klik vervolgens op **maken deelnemer**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Gebruiker maken][400]

3. <span data-ttu-id="2ff15-211">Op Hallo **is de relatie tussen - deelnemer maken** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2ff15-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Gebruiker maken][401]
    
    <span data-ttu-id="2ff15-213">a.</span><span class="sxs-lookup"><span data-stu-id="2ff15-213">a.</span></span> <span data-ttu-id="2ff15-214">Type Hallo vereiste kenmerken voor Britta Simon in de bijbehorende tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="2ff15-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="2ff15-215">De naam van de gebruiker van Britta kenmerk in PerformanceCentre moet Hallo hetzelfde als de gebruikersnaam Hallo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ff15-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="2ff15-216">b.</span><span class="sxs-lookup"><span data-stu-id="2ff15-216">b.</span></span> <span data-ttu-id="2ff15-217">Selecteer **Client Administrator** als **Kies rol**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="2ff15-218">c.</span><span class="sxs-lookup"><span data-stu-id="2ff15-218">c.</span></span> <span data-ttu-id="2ff15-219">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2ff15-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ff15-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2ff15-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPerformanceCentre toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2ff15-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2ff15-223">**tooassign Britta Simon tooPerformanceCentre, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2ff15-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ff15-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2ff15-226">Selecteer in de lijst met de toepassingen van Hallo **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="2ff15-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2ff15-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2ff15-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2ff15-230">Click **Add** button.</span></span> <span data-ttu-id="2ff15-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ff15-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2ff15-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ff15-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ff15-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ff15-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ff15-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ff15-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ff15-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2ff15-236">Testing single sign-on</span></span>

<span data-ttu-id="2ff15-237">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2ff15-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="2ff15-238">Als u op Hallo PerformanceCentre tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour PerformanceCentre toepassing.</span><span class="sxs-lookup"><span data-stu-id="2ff15-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ff15-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2ff15-239">Additional resources</span></span>

* [<span data-ttu-id="2ff15-240">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ff15-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ff15-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ff15-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

