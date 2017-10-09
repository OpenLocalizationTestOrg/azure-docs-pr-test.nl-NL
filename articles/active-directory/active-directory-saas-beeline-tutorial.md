---
title: 'Zelfstudie: Azure Active Directory-integratie met BeeLine | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BeeLine.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="3b10d-103">Zelfstudie: Azure Active Directory-integratie met BeeLine</span><span class="sxs-lookup"><span data-stu-id="3b10d-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="3b10d-104">In deze zelfstudie leert u hoe toointegrate BeeLine met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b10d-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b10d-105">BeeLine integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3b10d-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3b10d-106">U kunt beheren in Azure AD die tooBeeLine toegang heeft</span><span class="sxs-lookup"><span data-stu-id="3b10d-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="3b10d-107">U kunt uw gebruikers tooautomatically get aangemelde tooBeeLine (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3b10d-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b10d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3b10d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3b10d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3b10d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b10d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3b10d-110">Prerequisites</span></span>

<span data-ttu-id="3b10d-111">Azure AD-integratie met BeeLine tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3b10d-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="3b10d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3b10d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b10d-113">Een BeeLine eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3b10d-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b10d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3b10d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b10d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3b10d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b10d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3b10d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b10d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b10d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b10d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3b10d-118">Scenario description</span></span>
<span data-ttu-id="3b10d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3b10d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b10d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3b10d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b10d-121">Het toevoegen van BeeLine van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3b10d-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="3b10d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3b10d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="3b10d-123">Het toevoegen van BeeLine van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3b10d-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="3b10d-124">tooconfigure hello integratie van BeeLine in Azure AD, moet u tooadd BeeLine uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3b10d-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3b10d-125">**tooadd BeeLine via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3b10d-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b10d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3b10d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3b10d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3b10d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3b10d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3b10d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3b10d-133">Typ in het zoekvak Hallo **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-133">In hello search box, type **BeeLine**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="3b10d-135">Selecteer in het deelvenster resultaten hello, **BeeLine**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3b10d-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3b10d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3b10d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3b10d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BeeLine op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3b10d-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3b10d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BeeLine is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b10d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="3b10d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BeeLine toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3b10d-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="3b10d-141">Wijs in BeeLine, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="3b10d-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3b10d-142">tooconfigure en eenmalige aanmelding Azure AD-test met BeeLine, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3b10d-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3b10d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3b10d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3b10d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b10d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b10d-145">**[Maken van een testgebruiker BeeLine](#creating-a-beeline-test-user)**  -toohave een equivalent van Britta Simon in BeeLine die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3b10d-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b10d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3b10d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b10d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3b10d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3b10d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3b10d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3b10d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BeeLine configureren.</span><span class="sxs-lookup"><span data-stu-id="3b10d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="3b10d-150">**Azure AD tooconfigure eenmalige aanmelding met BeeLine, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3b10d-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b10d-151">In de Azure-portal op Hallo Hallo **BeeLine** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3b10d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3b10d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="3b10d-155">Op Hallo **BeeLine domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3b10d-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="3b10d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3b10d-157">a.</span></span> <span data-ttu-id="3b10d-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="3b10d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="3b10d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3b10d-159">b.</span></span> <span data-ttu-id="3b10d-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="3b10d-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="3b10d-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="3b10d-161">These values are not real.</span></span> <span data-ttu-id="3b10d-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="3b10d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="3b10d-163">Neem contact op met [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3b10d-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="3b10d-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3b10d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="3b10d-166">Uw toepassing Beeline verwacht Hallo SAML asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="3b10d-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="3b10d-167">Neem contact op met [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) eerste tooidentify Hallo juiste gebruikers-id die in de toepassing hello worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3b10d-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="3b10d-168">Ook Neem Hallo richtlijnen van [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) over Hallo kenmerk die ze willen toouse voor deze toewijzing.</span><span class="sxs-lookup"><span data-stu-id="3b10d-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="3b10d-169">U kunt Hallo-waarde van dit kenmerk beheren vanuit Hallo **gebruikerskenmerken** tabblad van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="3b10d-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="3b10d-170">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="3b10d-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="3b10d-171">Hier wordt de Hallo hebt toegewezen **gebruikers-id** claim met Hallo **userprincipalname** kenmerk unieke gebruikers-ID die wordt verzonden toohello Beeline toepassing in Hallo biedt elke geslaagde SAML Antwoord.</span><span class="sxs-lookup"><span data-stu-id="3b10d-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="3b10d-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3b10d-173">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3b10d-175">Op Hallo **BeeLine configuratie** sectie, klikt u op **configureren BeeLine** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3b10d-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3b10d-176">Kopiëren Hallo **Sign-Out URL** en **SAML entiteit-ID** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3b10d-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="3b10d-178">tooconfigure eenmalige aanmelding op **BeeLine** zijde, moet u toosend Hallo gedownload **Metadata XML** en **SAML entiteit-ID**, **Sign-Out URL**te[BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="3b10d-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="3b10d-179">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="3b10d-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3b10d-180">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="3b10d-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3b10d-181">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3b10d-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3b10d-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3b10d-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="3b10d-183">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3b10d-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3b10d-185">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3b10d-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b10d-186">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3b10d-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3b10d-188">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3b10d-190">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3b10d-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b10d-192">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3b10d-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3b10d-194">a.</span><span class="sxs-lookup"><span data-stu-id="3b10d-194">a.</span></span> <span data-ttu-id="3b10d-195">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b10d-196">b.</span><span class="sxs-lookup"><span data-stu-id="3b10d-196">b.</span></span> <span data-ttu-id="3b10d-197">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3b10d-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3b10d-198">c.</span><span class="sxs-lookup"><span data-stu-id="3b10d-198">c.</span></span> <span data-ttu-id="3b10d-199">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3b10d-200">d.</span><span class="sxs-lookup"><span data-stu-id="3b10d-200">d.</span></span> <span data-ttu-id="3b10d-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="3b10d-202">Een testgebruiker BeeLine maken</span><span class="sxs-lookup"><span data-stu-id="3b10d-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="3b10d-203">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Beeline maken.</span><span class="sxs-lookup"><span data-stu-id="3b10d-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="3b10d-204">Beeline toepassing moet alle Hallo gebruikers toobe ingericht in de toepassing hello voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3b10d-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="3b10d-205">Zo werken met Hallo [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) tooprovision deze gebruikers in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="3b10d-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3b10d-206">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b10d-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3b10d-207">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBeeLine toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="3b10d-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3b10d-209">**tooassign Britta Simon tooBeeLine, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3b10d-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b10d-210">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3b10d-212">Selecteer in de lijst met de toepassingen van Hallo **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-212">In hello applications list, select **BeeLine**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="3b10d-214">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3b10d-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3b10d-216">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3b10d-216">Click **Add** button.</span></span> <span data-ttu-id="3b10d-217">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3b10d-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3b10d-219">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b10d-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3b10d-220">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3b10d-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b10d-221">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3b10d-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3b10d-222">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3b10d-222">Testing single sign-on</span></span>

<span data-ttu-id="3b10d-223">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3b10d-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="3b10d-224">Als u op Hallo Beeline tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Beeline toepassing.</span><span class="sxs-lookup"><span data-stu-id="3b10d-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b10d-225">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3b10d-225">Additional resources</span></span>

* [<span data-ttu-id="3b10d-226">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b10d-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b10d-227">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3b10d-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

