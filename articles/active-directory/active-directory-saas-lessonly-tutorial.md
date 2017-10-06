---
title: 'Zelfstudie: Azure Active Directory-integratie met Lesson.ly | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Lesson.ly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="ec0d5-103">Zelfstudie: Azure Active Directory-integratie met Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="ec0d5-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="ec0d5-104">In deze zelfstudie leert u hoe toointegrate Lesson.ly met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec0d5-105">Lesson.ly integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ec0d5-106">U kunt beheren in Azure AD die tooLesson.ly toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ec0d5-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="ec0d5-107">U kunt uw gebruikers tooautomatically get aangemelde tooLesson.ly (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ec0d5-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec0d5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ec0d5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ec0d5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec0d5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec0d5-110">Prerequisites</span></span>

<span data-ttu-id="ec0d5-111">Azure AD-integratie met Lesson.ly tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="ec0d5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ec0d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec0d5-113">Een Lesson.ly eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ec0d5-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec0d5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec0d5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec0d5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec0d5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec0d5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ec0d5-118">Scenario description</span></span>
<span data-ttu-id="ec0d5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec0d5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec0d5-121">Het toevoegen van Lesson.ly van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ec0d5-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="ec0d5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec0d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="ec0d5-123">Het toevoegen van Lesson.ly van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ec0d5-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="ec0d5-124">tooconfigure hello integratie van Lesson.ly in Azure AD, moet u tooadd Lesson.ly uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ec0d5-125">**tooadd Lesson.ly via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ec0d5-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec0d5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec0d5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ec0d5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ec0d5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ec0d5-133">Typ in het zoekvak Hallo **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="ec0d5-135">Selecteer in het deelvenster resultaten hello, **Lesson.ly**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec0d5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec0d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec0d5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Lesson.ly op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec0d5-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Lesson.ly is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="ec0d5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Lesson.ly toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="ec0d5-141">Wijs in Lesson.ly, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ec0d5-142">tooconfigure en eenmalige aanmelding Azure AD-test met Lesson.ly, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ec0d5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ec0d5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec0d5-145">**[Maken van een testgebruiker Lesson.ly](#creating-a-lessonly-test-user)**  -toohave een equivalent van Britta Simon in Lesson.ly die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec0d5-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec0d5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec0d5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ec0d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec0d5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Lesson.ly configureren.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="ec0d5-150">**Azure AD tooconfigure eenmalige aanmelding met Lesson.ly, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ec0d5-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec0d5-151">In de Azure-portal op Hallo Hallo **Lesson.ly** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ec0d5-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="ec0d5-155">Op Hallo **Lesson.ly domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="ec0d5-157">a.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-157">a.</span></span> <span data-ttu-id="ec0d5-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="ec0d5-159">Wanneer een algemeen verwijst naar een naam die **NaamBedrijf** toobe vervangen door feitelijke naam nodig.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="ec0d5-160">b.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-160">b.</span></span> <span data-ttu-id="ec0d5-161">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="ec0d5-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-162">These values are not real.</span></span> <span data-ttu-id="ec0d5-163">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ec0d5-164">Neem contact op met [Lesson.ly Client ondersteuningsteam](mailto:dev@lessonly.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="ec0d5-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="ec0d5-167">Hallo Lesson.ly toepassing hello SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **SAML-Token kenmerken** configuration.hello volgende schermafbeelding ziet u een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="ec0d5-169">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="ec0d5-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ec0d5-170">Attribute Name</span></span>   | <span data-ttu-id="ec0d5-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ec0d5-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="ec0d5-172">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="ec0d5-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="ec0d5-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ec0d5-173">user.givenname</span></span> |
    | <span data-ttu-id="ec0d5-174">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="ec0d5-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="ec0d5-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="ec0d5-175">user.surname</span></span> |
    | <span data-ttu-id="ec0d5-176">urn: oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="ec0d5-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="ec0d5-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="ec0d5-177">user.mail</span></span> |

    <span data-ttu-id="ec0d5-178">a.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-178">a.</span></span> <span data-ttu-id="ec0d5-179">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ec0d5-182">b.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-182">b.</span></span> <span data-ttu-id="ec0d5-183">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="ec0d5-184">c.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-184">c.</span></span> <span data-ttu-id="ec0d5-185">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ec0d5-186">d.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-186">d.</span></span> <span data-ttu-id="ec0d5-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="ec0d5-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-188">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ec0d5-190">Op Hallo **Lesson.ly configuratie** sectie, klikt u op **configureren Lesson.ly** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ec0d5-191">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ec0d5-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="ec0d5-193">tooconfigure eenmalige aanmelding op **Lesson.ly** zijde, moet u toosend Hallo gedownload **Certificate(Base64)** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Lesson.ly ondersteuningsteam](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="ec0d5-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ec0d5-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ec0d5-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec0d5-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec0d5-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ec0d5-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec0d5-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ec0d5-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ec0d5-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec0d5-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec0d5-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec0d5-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec0d5-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec0d5-209">a.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-209">a.</span></span> <span data-ttu-id="ec0d5-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec0d5-211">b.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-211">b.</span></span> <span data-ttu-id="ec0d5-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec0d5-213">c.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-213">c.</span></span> <span data-ttu-id="ec0d5-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ec0d5-215">d.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-215">d.</span></span> <span data-ttu-id="ec0d5-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="ec0d5-217">Een testgebruiker Lesson.ly maken</span><span class="sxs-lookup"><span data-stu-id="ec0d5-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="ec0d5-218">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Lesson.ly van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="ec0d5-219">Lesson.LY ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ec0d5-220">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-220">There is no action item for you in this section.</span></span> <span data-ttu-id="ec0d5-221">Een nieuwe gebruiker wordt tijdens een poging tooaccess Lesson.ly gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="ec0d5-222">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Lesson.ly ondersteuningsteam](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ec0d5-223">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec0d5-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ec0d5-224">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLesson.ly toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ec0d5-226">**tooassign Britta Simon tooLesson.ly, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ec0d5-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec0d5-227">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ec0d5-229">Selecteer in de lijst met de toepassingen van Hallo **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="ec0d5-231">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ec0d5-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-233">Click **Add** button.</span></span> <span data-ttu-id="ec0d5-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ec0d5-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ec0d5-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec0d5-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec0d5-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ec0d5-239">Testing single sign-on</span></span>

<span data-ttu-id="ec0d5-240">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ec0d5-241">Als u op Hallo Lesson.ly tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Lesson.ly toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec0d5-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ec0d5-242">Additional resources</span></span>

* [<span data-ttu-id="ec0d5-243">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec0d5-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec0d5-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec0d5-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

