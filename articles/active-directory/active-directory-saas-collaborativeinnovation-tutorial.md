---
title: 'Zelfstudie: Azure Active Directory-integratie met samenwerking innovatie | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en gezamenlijke innovatie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="65f99-103">Zelfstudie: Azure Active Directory-integratie met samenwerking innovatie</span><span class="sxs-lookup"><span data-stu-id="65f99-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="65f99-104">In deze zelfstudie leert u hoe toointegrate gezamenlijke innovatie met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65f99-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65f99-105">Samenwerking innovatie integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="65f99-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65f99-106">U kunt beheren in Azure AD wie toegang tot tooCollaborative innovatie heeft</span><span class="sxs-lookup"><span data-stu-id="65f99-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="65f99-107">U kunt uw gebruikers tooautomatically get aangemelde tooCollaborative innovatie (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="65f99-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65f99-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="65f99-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65f99-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65f99-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65f99-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="65f99-110">Prerequisites</span></span>

<span data-ttu-id="65f99-111">Azure AD-integratie met samenwerking innovatie tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="65f99-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="65f99-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="65f99-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65f99-113">Een gezamenlijke innovatie eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="65f99-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65f99-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="65f99-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65f99-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="65f99-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65f99-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="65f99-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65f99-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65f99-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65f99-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="65f99-118">Scenario description</span></span>
<span data-ttu-id="65f99-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="65f99-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65f99-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="65f99-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65f99-121">Het toevoegen van samenwerking innovatie van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="65f99-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="65f99-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65f99-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="65f99-123">Het toevoegen van samenwerking innovatie van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="65f99-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="65f99-124">tooconfigure hello integratie van samenwerking innovatie in Azure AD, moet u tooadd gezamenlijke innovatie uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="65f99-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65f99-125">**tooadd gezamenlijke innovatie via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65f99-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f99-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="65f99-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65f99-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65f99-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65f99-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65f99-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="65f99-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65f99-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="65f99-133">Typ in het zoekvak Hallo **gezamenlijke innovatie**.</span><span class="sxs-lookup"><span data-stu-id="65f99-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="65f99-135">Selecteer in het deelvenster resultaten hello, **gezamenlijke innovatie**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="65f99-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65f99-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65f99-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65f99-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met samenwerking vernieuwing op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="65f99-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65f99-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in samenwerking vernieuwing is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65f99-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="65f99-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in samenwerking vernieuwing toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="65f99-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="65f99-141">In samenwerking vernieuwing Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="65f99-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65f99-142">tooconfigure en eenmalige aanmelding Azure AD-test met samenwerking innovatie, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65f99-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65f99-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="65f99-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65f99-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65f99-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65f99-145">**[Maken van een gezamenlijke innovatie testgebruiker](#creating-a-collaborative-innovation-test-user)**  -toohave een equivalent van Britta Simon in samenwerking vernieuwing die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="65f99-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65f99-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="65f99-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65f99-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="65f99-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65f99-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="65f99-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65f99-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing gezamenlijke innovatie configureren.</span><span class="sxs-lookup"><span data-stu-id="65f99-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="65f99-150">**Voer tooconfigure Azure AD eenmalige aanmelding met samenwerking innovatie Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65f99-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f99-151">In Azure-portal op Hallo Hallo **gezamenlijke innovatie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="65f99-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="65f99-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="65f99-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="65f99-155">Op Hallo **gezamenlijke innovatie domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65f99-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="65f99-157">a.</span><span class="sxs-lookup"><span data-stu-id="65f99-157">a.</span></span> <span data-ttu-id="65f99-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="65f99-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="65f99-159">b.</span><span class="sxs-lookup"><span data-stu-id="65f99-159">b.</span></span> <span data-ttu-id="65f99-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="65f99-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="65f99-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="65f99-161">These values are not real.</span></span> <span data-ttu-id="65f99-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="65f99-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="65f99-163">Neem contact op met [gezamenlijke innovatie Client ondersteuningsteam](https://www.unilever.com/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="65f99-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="65f99-164">Hallo SAML asserties verwacht gezamenlijk innovatie toepassingen in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="65f99-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="65f99-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="65f99-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="65f99-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="65f99-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="65f99-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="65f99-167">hello following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="65f99-169">Klik op **weergeven en alle andere gebruikerskenmerken bewerken** checkbox in Hallo **gebruikerskenmerken** sectie tooexpand Hallo kenmerken.</span><span class="sxs-lookup"><span data-stu-id="65f99-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="65f99-170">Volgende stappen uit op elke Hallo weergegeven kenmerken - Hallo uitvoeren</span><span class="sxs-lookup"><span data-stu-id="65f99-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="65f99-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="65f99-171">Attribute Name</span></span> | <span data-ttu-id="65f99-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="65f99-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="65f99-173">Voornaam</span><span class="sxs-lookup"><span data-stu-id="65f99-173">givenname</span></span> | <span data-ttu-id="65f99-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="65f99-174">user.givenname</span></span> |
    | <span data-ttu-id="65f99-175">Achternaam</span><span class="sxs-lookup"><span data-stu-id="65f99-175">surname</span></span> | <span data-ttu-id="65f99-176">User.surname</span><span class="sxs-lookup"><span data-stu-id="65f99-176">user.surname</span></span> |
    | <span data-ttu-id="65f99-177">EmailAddress</span><span class="sxs-lookup"><span data-stu-id="65f99-177">emailaddress</span></span> | <span data-ttu-id="65f99-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="65f99-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="65f99-179">naam</span><span class="sxs-lookup"><span data-stu-id="65f99-179">name</span></span> | <span data-ttu-id="65f99-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="65f99-180">user.userprincipalname</span></span> |

    <span data-ttu-id="65f99-181">a.</span><span class="sxs-lookup"><span data-stu-id="65f99-181">a.</span></span> <span data-ttu-id="65f99-182">Klik op Hallo kenmerk tooopen hello **kenmerk bewerken** venster.</span><span class="sxs-lookup"><span data-stu-id="65f99-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="65f99-184">b.</span><span class="sxs-lookup"><span data-stu-id="65f99-184">b.</span></span> <span data-ttu-id="65f99-185">Hallo URL waarde verwijderen uit Hallo **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="65f99-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="65f99-186">c.</span><span class="sxs-lookup"><span data-stu-id="65f99-186">c.</span></span> <span data-ttu-id="65f99-187">Klik op **Ok** toosave Hallo-instelling.</span><span class="sxs-lookup"><span data-stu-id="65f99-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="65f99-188">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="65f99-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="65f99-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="65f99-190">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="65f99-192">tooconfigure eenmalige aanmelding op **gezamenlijke innovatie** zijde, moet u toosend Hallo gedownload **Metadata XML** te[gezamenlijke innovatie ondersteuningsteam](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="65f99-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="65f99-193">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="65f99-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="65f99-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="65f99-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65f99-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="65f99-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65f99-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65f99-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65f99-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="65f99-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="65f99-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="65f99-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="65f99-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65f99-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f99-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="65f99-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65f99-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="65f99-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65f99-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="65f99-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65f99-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65f99-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65f99-209">a.</span><span class="sxs-lookup"><span data-stu-id="65f99-209">a.</span></span> <span data-ttu-id="65f99-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65f99-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65f99-211">b.</span><span class="sxs-lookup"><span data-stu-id="65f99-211">b.</span></span> <span data-ttu-id="65f99-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65f99-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65f99-213">c.</span><span class="sxs-lookup"><span data-stu-id="65f99-213">c.</span></span> <span data-ttu-id="65f99-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="65f99-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65f99-215">d.</span><span class="sxs-lookup"><span data-stu-id="65f99-215">d.</span></span> <span data-ttu-id="65f99-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="65f99-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="65f99-217">Maken van een gezamenlijke innovatie testgebruiker</span><span class="sxs-lookup"><span data-stu-id="65f99-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="65f99-218">Azure AD tooenable gebruikers toolog in tooCollaborative innovatie, ze in samenwerking innovatie moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="65f99-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="65f99-219">In geval van deze toepassing is inrichting automatische toepassing hello ondersteunt alleen in de tijd van gebruikersinrichting.</span><span class="sxs-lookup"><span data-stu-id="65f99-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="65f99-220">Er is daarom geen tooperform moeten alle volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="65f99-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65f99-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="65f99-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65f99-222">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCollaborative innovatie.</span><span class="sxs-lookup"><span data-stu-id="65f99-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="65f99-224">**tooassign Britta Simon tooCollaborative innovatie, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65f99-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f99-225">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65f99-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="65f99-227">Selecteer in de lijst met de toepassingen van Hallo **gezamenlijke innovatie**.</span><span class="sxs-lookup"><span data-stu-id="65f99-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="65f99-229">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="65f99-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="65f99-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="65f99-231">Click **Add** button.</span></span> <span data-ttu-id="65f99-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65f99-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="65f99-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="65f99-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65f99-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65f99-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65f99-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65f99-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65f99-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65f99-237">Testing single sign-on</span></span>

<span data-ttu-id="65f99-238">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="65f99-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65f99-239">Als u op Hallo gezamenlijke innovatie tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van samenwerking innovatie toepassing.</span><span class="sxs-lookup"><span data-stu-id="65f99-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="65f99-240">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65f99-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="65f99-241">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="65f99-241">Additional resources</span></span>

* [<span data-ttu-id="65f99-242">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65f99-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65f99-243">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65f99-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

