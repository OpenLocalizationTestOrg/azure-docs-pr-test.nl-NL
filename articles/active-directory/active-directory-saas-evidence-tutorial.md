---
title: 'Zelfstudie: Azure Active Directory-integratie met Evidence.com | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Evidence.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="012b5-103">Zelfstudie: Azure Active Directory-integratie met Evidence.com</span><span class="sxs-lookup"><span data-stu-id="012b5-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="012b5-104">In deze zelfstudie leert u hoe toointegrate Evidence.com met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="012b5-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="012b5-105">Evidence.com integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="012b5-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="012b5-106">U kunt beheren in Azure AD die tooEvidence.com toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="012b5-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="012b5-107">U kunt uw gebruikers tooautomatically get aangemelde tooEvidence.com (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="012b5-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="012b5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="012b5-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="012b5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="012b5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="012b5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="012b5-110">Prerequisites</span></span>

<span data-ttu-id="012b5-111">Azure AD-integratie met Evidence.com tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="012b5-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="012b5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="012b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="012b5-113">Een Evidence.com eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="012b5-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="012b5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="012b5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="012b5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="012b5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="012b5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="012b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="012b5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="012b5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="012b5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="012b5-118">Scenario description</span></span>
<span data-ttu-id="012b5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="012b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="012b5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="012b5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="012b5-121">Het toevoegen van Evidence.com van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="012b5-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="012b5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="012b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="012b5-123">Het toevoegen van Evidence.com van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="012b5-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="012b5-124">tooconfigure hello integratie van Evidence.com in Azure AD, moet u tooadd Evidence.com uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="012b5-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="012b5-125">**tooadd Evidence.com via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="012b5-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="012b5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="012b5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="012b5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="012b5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="012b5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="012b5-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="012b5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="012b5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="012b5-133">Typ in het zoekvak Hallo **Evidence.com**, selecteer **Evidence.com** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="012b5-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com in de lijst met resultaten Hallo](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="012b5-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="012b5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="012b5-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Evidence.com op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="012b5-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="012b5-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Evidence.com is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="012b5-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="012b5-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Evidence.com toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="012b5-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="012b5-139">Wijs in Evidence.com, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="012b5-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="012b5-140">tooconfigure en eenmalige aanmelding Azure AD-test met Evidence.com, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="012b5-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="012b5-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="012b5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="012b5-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="012b5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="012b5-143">**[Maak een testgebruiker Evidence.com](#create-a-evidencecom-test-user)**  -toohave een equivalent van Britta Simon in Evidence.com die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="012b5-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="012b5-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="012b5-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="012b5-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="012b5-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="012b5-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="012b5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="012b5-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Evidence.com configureren.</span><span class="sxs-lookup"><span data-stu-id="012b5-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="012b5-148">**Azure AD tooconfigure eenmalige aanmelding met Evidence.com, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="012b5-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="012b5-149">In de Azure-portal op Hallo Hallo **Evidence.com** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="012b5-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="012b5-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="012b5-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="012b5-153">Op Hallo **Evidence.com domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="012b5-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en evidence.com domein eenmalige aanmelding informatie](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="012b5-155">a.</span><span class="sxs-lookup"><span data-stu-id="012b5-155">a.</span></span> <span data-ttu-id="012b5-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="012b5-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="012b5-157">b.</span><span class="sxs-lookup"><span data-stu-id="012b5-157">b.</span></span> <span data-ttu-id="012b5-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="012b5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="012b5-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="012b5-159">These values are not real.</span></span> <span data-ttu-id="012b5-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="012b5-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="012b5-161">Neem contact op met [Evidence.com Client ondersteuningsteam](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="012b5-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="012b5-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="012b5-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="012b5-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="012b5-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="012b5-166">Op Hallo **Evidence.com configuratie** sectie, klikt u op **configureren Evidence.com** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="012b5-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="012b5-167">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="012b5-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Evidence.com configuratie](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="012b5-169">In een afzonderlijke browservenster aanmelding tooyour Evidence.com tenant als beheerder en te navigeren**Admin** tabblad</span><span class="sxs-lookup"><span data-stu-id="012b5-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="012b5-170">Klik op **Agency voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="012b5-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="012b5-171">Selecteer **SAML eenmalige aanmelding op basis van**</span><span class="sxs-lookup"><span data-stu-id="012b5-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="012b5-172">Kopiëren Hallo **SAML entiteit-ID**, **SAML Single Sign-On Service-URL** en **Sign-Out URL** waarden in hello Azure-portal en de overeenkomende velden toohello in Evidence.com wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="012b5-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="012b5-173">Open uw gedownloade Certificate(Base64)-bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **beveiligingscertificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="012b5-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="012b5-174">Hallo-configuratie op te slaan in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="012b5-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="012b5-175">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="012b5-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="012b5-176">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="012b5-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="012b5-177">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="012b5-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="012b5-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="012b5-178">Create an Azure AD test user</span></span>

<span data-ttu-id="012b5-179">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="012b5-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="012b5-181">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="012b5-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="012b5-182">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="012b5-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="012b5-184">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="012b5-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="012b5-186">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="012b5-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="012b5-188">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="012b5-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="012b5-190">a.</span><span class="sxs-lookup"><span data-stu-id="012b5-190">a.</span></span> <span data-ttu-id="012b5-191">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="012b5-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="012b5-192">b.</span><span class="sxs-lookup"><span data-stu-id="012b5-192">b.</span></span> <span data-ttu-id="012b5-193">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="012b5-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="012b5-194">c.</span><span class="sxs-lookup"><span data-stu-id="012b5-194">c.</span></span> <span data-ttu-id="012b5-195">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="012b5-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="012b5-196">d.</span><span class="sxs-lookup"><span data-stu-id="012b5-196">d.</span></span> <span data-ttu-id="012b5-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="012b5-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="012b5-198">Een testgebruiker Evidence.com maken</span><span class="sxs-lookup"><span data-stu-id="012b5-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="012b5-199">Azure AD gebruikers toobe kunnen toosign in, als ze worden ingericht om toegang te krijgen in Hallo Evidence.com toepassing.</span><span class="sxs-lookup"><span data-stu-id="012b5-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="012b5-200">Deze sectie wordt beschreven hoe toocreate Azure AD gebruikersaccounts in Evidence.com</span><span class="sxs-lookup"><span data-stu-id="012b5-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="012b5-201">**een gebruikersaccount in Evidence.com tooprovision:**</span><span class="sxs-lookup"><span data-stu-id="012b5-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="012b5-202">In een browservenster geopend, meld u bij uw bedrijf Evidence.com site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="012b5-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="012b5-203">Navigeer te**Admin** tabblad.</span><span class="sxs-lookup"><span data-stu-id="012b5-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="012b5-204">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="012b5-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="012b5-205">Klik op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="012b5-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="012b5-206">Hallo **e-mailadres** Hallo toegevoegd gebruiker moet overeenkomen met de gebruikersnaam Hallo Hallo gebruikers in Azure AD die u wenst dat toogive toegang.</span><span class="sxs-lookup"><span data-stu-id="012b5-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="012b5-207">Als het Hallo-gebruikersnaam en e-mailadres zijn niet dezelfde waarde in uw organisatie hello, kunt u Hallo **Evidence.com > kenmerken > eenmalige aanmelding** sectie van hello Azure portal toochange hello nameidenitifer verzonden tooEvidence.com toobe Hallo e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="012b5-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="012b5-208">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="012b5-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="012b5-209">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEvidence.com toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="012b5-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="012b5-211">**tooassign Britta Simon tooEvidence.com, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="012b5-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="012b5-212">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="012b5-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="012b5-214">Selecteer in de lijst met de toepassingen van Hallo **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="012b5-214">In hello applications list, select **Evidence.com**.</span></span>

    ![Hallo Evidence.com koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="012b5-216">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="012b5-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="012b5-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="012b5-218">Click **Add** button.</span></span> <span data-ttu-id="012b5-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="012b5-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="012b5-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="012b5-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="012b5-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="012b5-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="012b5-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="012b5-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="012b5-224">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="012b5-224">Test single sign-on</span></span>

<span data-ttu-id="012b5-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="012b5-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="012b5-226">Als u op Hallo Evidence.com tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Evidence.com toepassing.</span><span class="sxs-lookup"><span data-stu-id="012b5-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="012b5-227">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="012b5-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="012b5-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="012b5-228">Additional resources</span></span>

* [<span data-ttu-id="012b5-229">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="012b5-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="012b5-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="012b5-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

