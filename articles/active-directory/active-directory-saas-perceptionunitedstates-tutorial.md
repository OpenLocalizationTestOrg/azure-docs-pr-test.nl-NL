---
title: 'Zelfstudie: Azure Active Directory-integratie met perceptie Verenigde Staten (niet-UltiPro) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en perceptie Verenigde Staten (niet-UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="ff3cd-103">Zelfstudie: Azure Active Directory-integratie met perceptie Verenigde Staten (niet-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="ff3cd-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="ff3cd-104">In deze zelfstudie leert u hoe toointegrate perceptie Verenigde Staten (niet-UltiPro) met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff3cd-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff3cd-105">Perceptie Verenigde Staten (niet-UltiPro) integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ff3cd-106">U kunt beheren in Azure AD die toegang tooPerception Verenigde Staten (niet-UltiPro) heeft.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="ff3cd-107">U kunt uw gebruikers tooautomatically get aangemelde tooPerception Verenigde Staten (niet-UltiPro) (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ff3cd-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ff3cd-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff3cd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff3cd-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ff3cd-110">Prerequisites</span></span>

<span data-ttu-id="ff3cd-111">tooconfigure Azure AD-integratie met perceptie Verenigde Staten (niet-UltiPro), moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="ff3cd-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ff3cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff3cd-113">Een perceptie Verenigde Staten (niet-UltiPro) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ff3cd-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff3cd-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff3cd-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff3cd-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff3cd-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff3cd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff3cd-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ff3cd-118">Scenario description</span></span>
<span data-ttu-id="ff3cd-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff3cd-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff3cd-121">Perceptie Verenigde Staten (niet-UltiPro) uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="ff3cd-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="ff3cd-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ff3cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="ff3cd-123">Perceptie Verenigde Staten (niet-UltiPro) uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="ff3cd-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="ff3cd-124">tooconfigure hello integratie van perceptie Verenigde Staten (niet-UltiPro) in Azure AD, moet u tooadd perceptie Verenigde Staten (niet-UltiPro) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ff3cd-125">**tooadd perceptie Verenigde Staten (niet-UltiPro) uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ff3cd-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff3cd-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="ff3cd-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ff3cd-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="ff3cd-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="ff3cd-133">Typ in het zoekvak Hallo **perceptie Verenigde Staten (niet-UltiPro)**, selecteer **perceptie Verenigde Staten (niet-UltiPro)** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Perceptie Verenigde Staten (niet-UltiPro) in de lijst met resultaten Hallo](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ff3cd-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff3cd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ff3cd-136">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met perceptie Verenigde Staten (niet-UltiPro) op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff3cd-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in perceptie Verenigde Staten (niet-UltiPro) is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="ff3cd-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in de perceptie Verenigde Staten (niet-UltiPro) toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="ff3cd-139">In perceptie Verenigde Staten (niet-UltiPro), wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ff3cd-140">tooconfigure en test eenmalige aanmelding Azure AD met perceptie Verenigde Staten (niet-UltiPro), moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ff3cd-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ff3cd-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff3cd-143">**[Maak een testgebruiker perceptie Verenigde Staten (niet-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave een equivalent van Britta Simon in perceptie Verenigde Staten (niet-UltiPro) die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff3cd-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff3cd-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ff3cd-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ff3cd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ff3cd-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing perceptie Verenigde Staten (niet-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="ff3cd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="ff3cd-148">**Azure AD tooconfigure eenmalige aanmelding met perceptie Verenigde Staten (niet-UltiPro) uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ff3cd-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="ff3cd-149">In de Azure-portal op Hallo Hallo **perceptie Verenigde Staten (niet-UltiPro)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ff3cd-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="ff3cd-153">Op Hallo **perceptie Verenigde Staten (niet-UltiPro)-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Perceptie Verenigde Staten (niet-UltiPro)-domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="ff3cd-155">a.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-155">a.</span></span> <span data-ttu-id="ff3cd-156">In Hallo **id** textbox type Hallo URL:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="ff3cd-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="ff3cd-157">b.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-157">b.</span></span> <span data-ttu-id="ff3cd-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="ff3cd-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ff3cd-159">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-159">hello value is not real.</span></span> <span data-ttu-id="ff3cd-160">Hallo-waarde wordt bijgewerkt met Hallo werkelijke antwoord-URL, die verderop in Hallo zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="ff3cd-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="ff3cd-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-163">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff3cd-165">Op Hallo **perceptie Verenigde Staten (niet-UltiPro) configuratie** sectie, klikt u op **configureren perceptie Verenigde Staten (niet-UltiPro)** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ff3cd-166">Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ff3cd-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="ff3cd-167">a.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-167">a.</span></span> <span data-ttu-id="ff3cd-168">Hallo **perceptie Verenigde Staten (niet-UltiPro)** toepassing hello vereist **SAML entiteit-ID** waarde, die u hebt gekopieerd, toobe uri-codering.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="ff3cd-169">tooget hello uri-gecodeerde waarde gebruik Hallo volgende koppeling:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="ff3cd-170">b.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-170">b.</span></span> <span data-ttu-id="ff3cd-171">Nadat u de uri Hallo gecodeerde waarde combineren met Hallo **antwoord-URL** zoals vermeld hieronder -</span><span class="sxs-lookup"><span data-stu-id="ff3cd-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="ff3cd-172">c.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-172">c.</span></span> <span data-ttu-id="ff3cd-173">Plakken Hallo hierboven waarde in Hallo **antwoord-URL** textbox in **perceptie Verenigde Staten (niet-UltiPro)-domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Perceptie Verenigde Staten (niet-UltiPro)-configuratie](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="ff3cd-175">Een ander browservenster geopend Meld u aan bij tooyour perceptie Verenigde Staten (niet-UltiPro) bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="ff3cd-176">Klik in het Hallo hoofdwerkbalk op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Perceptie Verenigde Staten (niet-UltiPro) gebruiker](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="ff3cd-178">Op Hallo **Accountinstellingen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Perceptie Verenigde Staten (niet-UltiPro) gebruiker](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="ff3cd-180">a.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-180">a.</span></span> <span data-ttu-id="ff3cd-181">In Hallo **bedrijfsnaam** textbox Hallo typenaam Hallo **bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="ff3cd-182">b.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-182">b.</span></span> <span data-ttu-id="ff3cd-183">In Hallo **accountnaam** textbox Hallo typenaam Hallo **Account**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="ff3cd-184">c.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-184">c.</span></span> <span data-ttu-id="ff3cd-185">In **standaard antwoord-tooEmail** tekstvak, type Hallo geldig **e**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="ff3cd-186">d.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-186">d.</span></span> <span data-ttu-id="ff3cd-187">Selecteer **SSO-identiteitsprovider** als **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="ff3cd-188">Op Hallo **SSO configuratie** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![Perceptie Verenigde Staten (niet-UltiPro) SSOConfig](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="ff3cd-190">a.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-190">a.</span></span> <span data-ttu-id="ff3cd-191">Selecteer **SAML NameID Type** als **e**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="ff3cd-192">b.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-192">b.</span></span> <span data-ttu-id="ff3cd-193">In Hallo **SSO configuratienaam** textbox Hallo-typenaam van uw **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="ff3cd-194">c.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-194">c.</span></span> <span data-ttu-id="ff3cd-195">In **identiteit providernaam** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ff3cd-196">d.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-196">d.</span></span> <span data-ttu-id="ff3cd-197">In **SAML domein textbox**, Voer Hallo domein zoals  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ff3cd-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="ff3cd-198">e.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-198">e.</span></span> <span data-ttu-id="ff3cd-199">Klik op **opnieuw uploaden** tooupload hello **Metadata XML** bestand.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="ff3cd-200">f.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-200">f.</span></span> <span data-ttu-id="ff3cd-201">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="ff3cd-202">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ff3cd-203">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ff3cd-204">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff3cd-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ff3cd-205">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ff3cd-205">Create an Azure AD test user</span></span>

<span data-ttu-id="ff3cd-206">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="ff3cd-208">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ff3cd-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff3cd-209">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ff3cd-211">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ff3cd-213">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ff3cd-215">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff3cd-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ff3cd-217">a.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-217">a.</span></span> <span data-ttu-id="ff3cd-218">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff3cd-219">b.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-219">b.</span></span> <span data-ttu-id="ff3cd-220">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ff3cd-221">c.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-221">c.</span></span> <span data-ttu-id="ff3cd-222">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ff3cd-223">d.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-223">d.</span></span> <span data-ttu-id="ff3cd-224">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="ff3cd-225">Maak een testgebruiker perceptie Verenigde Staten (niet-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="ff3cd-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="ff3cd-226">In deze sectie maakt u een gebruiker met de naam Britta Simon in perceptie Verenigde Staten (niet-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="ff3cd-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="ff3cd-227">Werken met [ondersteuningsteam perceptie Verenigde Staten (niet-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd Hallo gebruikers in Hallo perceptie Verenigde Staten (niet-UltiPro) platform.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ff3cd-228">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff3cd-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ff3cd-229">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooPerception Verenigde Staten (niet-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="ff3cd-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="ff3cd-231">**tooassign Britta Simon tooPerception Verenigde Staten (niet-UltiPro), Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ff3cd-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="ff3cd-232">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ff3cd-234">Selecteer in de lijst met de toepassingen van Hallo **perceptie Verenigde Staten (niet-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![Hallo perceptie Verenigde Staten (niet-UltiPro) koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="ff3cd-236">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="ff3cd-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-238">Click **Add** button.</span></span> <span data-ttu-id="ff3cd-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="ff3cd-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ff3cd-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff3cd-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ff3cd-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ff3cd-244">Test single sign-on</span></span>

<span data-ttu-id="ff3cd-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ff3cd-246">Als u op Hallo perceptie Verenigde Staten (niet-UltiPro)-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour perceptie Verenigde Staten (niet-UltiPro)-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff3cd-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="ff3cd-247">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ff3cd-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ff3cd-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ff3cd-248">Additional resources</span></span>

* [<span data-ttu-id="ff3cd-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff3cd-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff3cd-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff3cd-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

