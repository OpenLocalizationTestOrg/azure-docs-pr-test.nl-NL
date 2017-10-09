---
title: 'Zelfstudie: Azure Active Directory-integratie met IdeaScale | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en IdeaScale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="770a2-103">Zelfstudie: Azure Active Directory-integratie met IdeaScale</span><span class="sxs-lookup"><span data-stu-id="770a2-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="770a2-104">In deze zelfstudie leert u hoe toointegrate IdeaScale met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="770a2-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="770a2-105">IdeaScale integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="770a2-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="770a2-106">U kunt beheren in Azure AD die tooIdeaScale toegang heeft</span><span class="sxs-lookup"><span data-stu-id="770a2-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="770a2-107">U kunt uw gebruikers tooautomatically get aangemelde tooIdeaScale (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="770a2-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="770a2-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="770a2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="770a2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="770a2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="770a2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="770a2-110">Prerequisites</span></span>

<span data-ttu-id="770a2-111">Azure AD-integratie met IdeaScale tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="770a2-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="770a2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="770a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="770a2-113">Een IdeaScale eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="770a2-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="770a2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="770a2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="770a2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="770a2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="770a2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="770a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="770a2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="770a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="770a2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="770a2-118">Scenario description</span></span>
<span data-ttu-id="770a2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="770a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="770a2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="770a2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="770a2-121">Het toevoegen van IdeaScale van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="770a2-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="770a2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="770a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="770a2-123">Het toevoegen van IdeaScale van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="770a2-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="770a2-124">tooconfigure hello integratie van IdeaScale in Azure AD, moet u tooadd IdeaScale uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="770a2-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="770a2-125">**tooadd IdeaScale via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="770a2-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a2-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="770a2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="770a2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="770a2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="770a2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="770a2-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="770a2-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="770a2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="770a2-133">Typ in het zoekvak Hallo **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="770a2-133">In hello search box, type **IdeaScale**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="770a2-135">Selecteer in het deelvenster resultaten hello, **IdeaScale**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="770a2-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="770a2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="770a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="770a2-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met IdeaScale op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="770a2-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="770a2-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in IdeaScale is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="770a2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="770a2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in IdeaScale toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="770a2-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="770a2-141">Wijs in IdeaScale, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="770a2-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="770a2-142">tooconfigure en eenmalige aanmelding Azure AD-test met IdeaScale, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="770a2-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="770a2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="770a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="770a2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="770a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="770a2-145">**[Maken van een testgebruiker IdeaScale](#creating-an-ideascale-test-user)**  -toohave een equivalent van Britta Simon in IdeaScale die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="770a2-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="770a2-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="770a2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="770a2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="770a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="770a2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="770a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="770a2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing IdeaScale configureren.</span><span class="sxs-lookup"><span data-stu-id="770a2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="770a2-150">**Azure AD tooconfigure eenmalige aanmelding met IdeaScale, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="770a2-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a2-151">In de Azure-portal op Hallo Hallo **IdeaScale** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="770a2-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="770a2-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="770a2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="770a2-155">Op Hallo **IdeaScale domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="770a2-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="770a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="770a2-157">a.</span></span> <span data-ttu-id="770a2-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="770a2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="770a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="770a2-159">b.</span></span> <span data-ttu-id="770a2-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="770a2-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="770a2-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="770a2-161">These values are not real.</span></span> <span data-ttu-id="770a2-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="770a2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="770a2-163">Neem contact op met [IdeaScale Client ondersteuningsteam](http://support.ideascale.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="770a2-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="770a2-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="770a2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="770a2-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="770a2-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="770a2-168">Op Hallo **IdeaScale configuratie** sectie, klikt u op **configureren IdeaScale** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="770a2-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="770a2-169">Kopiëren Hallo **Sign-Out-URL en de entiteit-ID SAML** van Hallo **Naslaggids punt**.</span><span class="sxs-lookup"><span data-stu-id="770a2-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="770a2-171">In een ander browservenster, meld u aan tooyour IdeaScale bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="770a2-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="770a2-172">Ga te**Community instellingen**.</span><span class="sxs-lookup"><span data-stu-id="770a2-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="770a2-173">![Instellingen van de community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community-instellingen")</span><span class="sxs-lookup"><span data-stu-id="770a2-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="770a2-174">Ga te**beveiliging \> instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="770a2-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="770a2-175">![Eenmalige aanmelding instellingen](./media/active-directory-saas-ideascale-tutorial/ic790848.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="770a2-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="770a2-176">Als **eenmaal aanmelden Type**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="770a2-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="770a2-177">![Eenmalige aanmelding Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "eenmalige aanmelding Type")</span><span class="sxs-lookup"><span data-stu-id="770a2-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="770a2-178">Op Hallo **instellingen voor eenmalige aanmelding** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="770a2-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="770a2-179">![Eenmalige aanmelding instellingen](./media/active-directory-saas-ideascale-tutorial/ic790850.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="770a2-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="770a2-180">a.</span><span class="sxs-lookup"><span data-stu-id="770a2-180">a.</span></span> <span data-ttu-id="770a2-181">In **SAML IdP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="770a2-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="770a2-182">b.</span><span class="sxs-lookup"><span data-stu-id="770a2-182">b.</span></span> <span data-ttu-id="770a2-183">Hallo-inhoud van uw van het gedownloade metagegevensbestand kopiëren vanuit Azure-portal en plak deze in Hallo **SAML IdP metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="770a2-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="770a2-184">c.</span><span class="sxs-lookup"><span data-stu-id="770a2-184">c.</span></span> <span data-ttu-id="770a2-185">In **afmelding geslaagd URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="770a2-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="770a2-186">d.</span><span class="sxs-lookup"><span data-stu-id="770a2-186">d.</span></span> <span data-ttu-id="770a2-187">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="770a2-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="770a2-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="770a2-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="770a2-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="770a2-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="770a2-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="770a2-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="770a2-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="770a2-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="770a2-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="770a2-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="770a2-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="770a2-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a2-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="770a2-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="770a2-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="770a2-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="770a2-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="770a2-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="770a2-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="770a2-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="770a2-203">a.</span><span class="sxs-lookup"><span data-stu-id="770a2-203">a.</span></span> <span data-ttu-id="770a2-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="770a2-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="770a2-205">b.</span><span class="sxs-lookup"><span data-stu-id="770a2-205">b.</span></span> <span data-ttu-id="770a2-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="770a2-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="770a2-207">c.</span><span class="sxs-lookup"><span data-stu-id="770a2-207">c.</span></span> <span data-ttu-id="770a2-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="770a2-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="770a2-209">d.</span><span class="sxs-lookup"><span data-stu-id="770a2-209">d.</span></span> <span data-ttu-id="770a2-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="770a2-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="770a2-211">Een testgebruiker IdeaScale maken</span><span class="sxs-lookup"><span data-stu-id="770a2-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="770a2-212">Azure AD tooenable gebruikers toolog in IdeaScale, ze in tooIdeaScale moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="770a2-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="770a2-213">In geval van IdeaScale Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="770a2-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="770a2-214">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="770a2-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a2-215">Meld u bij tooyour **IdeaScale** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="770a2-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="770a2-216">Ga te**Community instellingen**.</span><span class="sxs-lookup"><span data-stu-id="770a2-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="770a2-217">![Instellingen van de community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community-instellingen")</span><span class="sxs-lookup"><span data-stu-id="770a2-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="770a2-218">Ga te**basisinstellingen \> lid Management**.</span><span class="sxs-lookup"><span data-stu-id="770a2-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="770a2-219">Klik op **lid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="770a2-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="770a2-220">![Lid Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "lid Management")</span><span class="sxs-lookup"><span data-stu-id="770a2-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="770a2-221">Voer in Hallo sectie Nieuw lid toevoegt, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="770a2-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="770a2-222">![Nieuw lid toevoegt](./media/active-directory-saas-ideascale-tutorial/ic790853.png "nieuw lid toevoegt")</span><span class="sxs-lookup"><span data-stu-id="770a2-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="770a2-223">a.</span><span class="sxs-lookup"><span data-stu-id="770a2-223">a.</span></span> <span data-ttu-id="770a2-224">In Hallo **e-mailadressen** textbox type Hallo e-mailadres van een geldige AAD-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="770a2-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="770a2-225">b.</span><span class="sxs-lookup"><span data-stu-id="770a2-225">b.</span></span> <span data-ttu-id="770a2-226">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="770a2-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="770a2-227">Hello Azure Active Directory-accounthouder Hiermee haalt u een e-mail met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="770a2-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="770a2-228">U kunt andere IdeaScale gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door IdeaScale tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="770a2-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="770a2-229">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="770a2-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="770a2-230">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooIdeaScale toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="770a2-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="770a2-232">**tooassign Britta Simon tooIdeaScale, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="770a2-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="770a2-233">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="770a2-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="770a2-235">Selecteer in de lijst met de toepassingen van Hallo **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="770a2-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="770a2-237">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="770a2-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="770a2-239">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="770a2-239">Click **Add** button.</span></span> <span data-ttu-id="770a2-240">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="770a2-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="770a2-242">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="770a2-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="770a2-243">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="770a2-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="770a2-244">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="770a2-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="770a2-245">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="770a2-245">Testing single sign-on</span></span>


<span data-ttu-id="770a2-246">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="770a2-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="770a2-247">Als u op Hallo IdeaScale tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour IdeaScale toepassing.</span><span class="sxs-lookup"><span data-stu-id="770a2-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="770a2-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="770a2-248">Additional resources</span></span>

* [<span data-ttu-id="770a2-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="770a2-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="770a2-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="770a2-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

