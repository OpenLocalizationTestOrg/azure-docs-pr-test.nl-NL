---
title: 'Zelfstudie: Azure Active Directory-integratie met Schoolbord meer | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Schoolbord meer informatie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="79405-103">Zelfstudie: Azure Active Directory-integratie met Schoolbord meer</span><span class="sxs-lookup"><span data-stu-id="79405-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="79405-104">In deze zelfstudie leert u hoe toointegrate Schoolbord meer met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79405-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79405-105">Schoolbord meer integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="79405-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79405-106">U kunt beheren in Azure AD wie toegang tot tooBlackboard meer informatie heeft</span><span class="sxs-lookup"><span data-stu-id="79405-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="79405-107">U kunt uw gebruikers tooautomatically get aangemelde tooBlackboard meer (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="79405-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79405-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="79405-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79405-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79405-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79405-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="79405-110">Prerequisites</span></span>

<span data-ttu-id="79405-111">Azure AD-integratie met Schoolbord meer tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="79405-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="79405-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="79405-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79405-113">Een Schoolbord meer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="79405-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79405-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="79405-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79405-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="79405-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79405-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="79405-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79405-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79405-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79405-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="79405-118">Scenario description</span></span>
<span data-ttu-id="79405-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="79405-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79405-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="79405-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79405-121">Schoolbord meer informatie over het toevoegen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="79405-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="79405-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79405-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="79405-123">Schoolbord meer informatie over het toevoegen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="79405-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="79405-124">tooconfigure hello integratie van Schoolbord meer in Azure AD, moet u tooadd Schoolbord meer uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="79405-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79405-125">**tooadd Schoolbord meer via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79405-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79405-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="79405-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79405-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79405-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79405-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79405-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="79405-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79405-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="79405-133">Typ in het zoekvak Hallo **Schoolbord meer**.</span><span class="sxs-lookup"><span data-stu-id="79405-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="79405-135">Selecteer in het deelvenster resultaten hello, **Schoolbord meer**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="79405-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79405-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79405-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79405-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Schoolbord meer op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="79405-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79405-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Schoolbord meer is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79405-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="79405-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Schoolbord meer toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="79405-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="79405-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Schoolbord meer informatie.</span><span class="sxs-lookup"><span data-stu-id="79405-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="79405-142">tooconfigure en eenmalige aanmelding Azure AD-test met Schoolbord meer, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79405-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79405-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="79405-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79405-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79405-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79405-145">**[Maken van een testgebruiker Schoolbord meer](#creating-a-blackboard-learn-test-user)**  -toohave een equivalent van Britta Simon in Schoolbord informatie die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="79405-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79405-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="79405-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79405-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="79405-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79405-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="79405-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79405-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Schoolbord meer informatie.</span><span class="sxs-lookup"><span data-stu-id="79405-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="79405-150">**tooconfigure Azure AD eenmalige aanmelding met Schoolbord meer wilt weten, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79405-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="79405-151">In Azure-portal op Hallo Hallo **Schoolbord meer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="79405-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="79405-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="79405-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="79405-155">Op Hallo **Schoolbord meer informatie over domein- en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79405-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="79405-157">a.</span><span class="sxs-lookup"><span data-stu-id="79405-157">a.</span></span> <span data-ttu-id="79405-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="79405-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="79405-159">b.</span><span class="sxs-lookup"><span data-stu-id="79405-159">b.</span></span> <span data-ttu-id="79405-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="79405-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="79405-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="79405-161">These values are not real.</span></span> <span data-ttu-id="79405-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="79405-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="79405-163">Neem contact op met [Schoolbord meer informatie over Client-ondersteuningsteam](https://www.blackboard.com/support/index.aspx) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="79405-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="79405-164">Hallo SAML asserties verwacht Schoolbord meer toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="79405-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="79405-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="79405-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="79405-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="79405-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="79405-167">Hallo volgende Schermafbeelding toont een voorbeeld over het.</span><span class="sxs-lookup"><span data-stu-id="79405-167">hello following screenshot shows an example about it.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="79405-169">In Hallo **gebruikerskenmerken** sectie op **eenmalige aanmelding** dialoogvenster SAML-token kenmerken configureren, zoals in afbeelding Hallo en Hallo volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="79405-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="79405-170">We hebben Hallo Userprincipalname toegewezen als Hallo unieke gebruikerskenmerk hier, maar u toohello geschikte waarde, die uniek is voor gebruiker in de organisatie Hallo Hallo en die wordt toegewezen tooBlackboard meer gebruikersnaamvelden kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="79405-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="79405-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="79405-171">Attribute Name</span></span> | <span data-ttu-id="79405-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="79405-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="79405-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="79405-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="79405-174">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="79405-174">user.userprincipalname</span></span> |

    <span data-ttu-id="79405-175">a.</span><span class="sxs-lookup"><span data-stu-id="79405-175">a.</span></span> <span data-ttu-id="79405-176">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79405-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="79405-179">b.</span><span class="sxs-lookup"><span data-stu-id="79405-179">b.</span></span> <span data-ttu-id="79405-180">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="79405-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="79405-181">c.</span><span class="sxs-lookup"><span data-stu-id="79405-181">c.</span></span> <span data-ttu-id="79405-182">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="79405-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="79405-183">d.</span><span class="sxs-lookup"><span data-stu-id="79405-183">d.</span></span> <span data-ttu-id="79405-184">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="79405-184">Click **Ok**.</span></span>

4. <span data-ttu-id="79405-185">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="79405-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="79405-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="79405-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="79405-189">Op Hallo **Schoolbord meer configuratie** sectie, klikt u op **configureren Schoolbord meer** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="79405-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="79405-190">Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="79405-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="79405-192">tooconfigure eenmalige aanmelding op **Schoolbord meer** zijde, moet u toosend Hallo gedownload **Metadata XML** en **SAML entiteit-ID** te[Schoolbord meer ondersteuning voor](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="79405-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="79405-193">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="79405-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79405-194">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="79405-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79405-195">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79405-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79405-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="79405-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="79405-197">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="79405-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="79405-199">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79405-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79405-200">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="79405-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79405-202">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="79405-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79405-204">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="79405-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79405-206">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="79405-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79405-208">a.</span><span class="sxs-lookup"><span data-stu-id="79405-208">a.</span></span> <span data-ttu-id="79405-209">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79405-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79405-210">b.</span><span class="sxs-lookup"><span data-stu-id="79405-210">b.</span></span> <span data-ttu-id="79405-211">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79405-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="79405-212">c.</span><span class="sxs-lookup"><span data-stu-id="79405-212">c.</span></span> <span data-ttu-id="79405-213">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="79405-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79405-214">d.</span><span class="sxs-lookup"><span data-stu-id="79405-214">d.</span></span> <span data-ttu-id="79405-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="79405-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="79405-216">Maken van een testgebruiker Schoolbord meer</span><span class="sxs-lookup"><span data-stu-id="79405-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="79405-217">In deze sectie kunt u een gebruiker met de naam van Britta Simon in Schoolbord meer maken.</span><span class="sxs-lookup"><span data-stu-id="79405-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="79405-218">Schoolbord meer toepassing ondersteunt alleen in de tijd van gebruikersinrichting.</span><span class="sxs-lookup"><span data-stu-id="79405-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="79405-219">Zorg ervoor dat u Hallo claims hebt geconfigureerd zoals beschreven in de sectie Hallo  **[eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="79405-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79405-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="79405-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79405-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooBlackboard meer informatie.</span><span class="sxs-lookup"><span data-stu-id="79405-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="79405-223">**tooassign Britta Simon tooBlackboard meer, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="79405-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="79405-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="79405-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="79405-226">Selecteer in de lijst met de toepassingen van Hallo **Schoolbord meer**.</span><span class="sxs-lookup"><span data-stu-id="79405-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="79405-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="79405-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="79405-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="79405-230">Click **Add** button.</span></span> <span data-ttu-id="79405-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79405-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="79405-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="79405-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79405-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79405-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79405-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="79405-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79405-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="79405-236">Testing single sign-on</span></span>

<span data-ttu-id="79405-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="79405-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79405-238">Als u op Hallo Schoolbord meer tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Schoolbord meer toepassing.</span><span class="sxs-lookup"><span data-stu-id="79405-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="79405-239">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79405-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="79405-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="79405-240">Additional resources</span></span>

* [<span data-ttu-id="79405-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79405-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79405-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79405-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

