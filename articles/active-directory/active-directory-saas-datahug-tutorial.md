---
title: 'Zelfstudie: Azure Active Directory-integratie met Datahug | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Datahug.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="2c6c5-103">Zelfstudie: Azure Active Directory-integratie met Datahug</span><span class="sxs-lookup"><span data-stu-id="2c6c5-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="2c6c5-104">In deze zelfstudie leert u hoe toointegrate Datahug met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2c6c5-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2c6c5-105">Datahug integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2c6c5-106">U kunt beheren in Azure AD die tooDatahug toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2c6c5-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="2c6c5-107">U kunt uw gebruikers tooautomatically get aangemelde tooDatahug (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c6c5-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2c6c5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2c6c5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2c6c5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="2c6c5-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2c6c5-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c6c5-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c6c5-111">Prerequisites</span></span>

<span data-ttu-id="2c6c5-112">Azure AD-integratie met Datahug tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="2c6c5-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2c6c5-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2c6c5-114">Een Datahug eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2c6c5-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2c6c5-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2c6c5-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2c6c5-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2c6c5-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c6c5-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2c6c5-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2c6c5-119">Scenario description</span></span>
<span data-ttu-id="2c6c5-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2c6c5-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2c6c5-122">Het toevoegen van Datahug van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2c6c5-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="2c6c5-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c6c5-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="2c6c5-124">Het toevoegen van Datahug van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2c6c5-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="2c6c5-125">tooconfigure hello integratie van Datahug in Azure AD, moet u tooadd Datahug uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2c6c5-126">**tooadd Datahug via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c6c5-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c6c5-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2c6c5-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2c6c5-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2c6c5-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2c6c5-134">Typ in het zoekvak Hallo **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-134">In hello search box, type **Datahug**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="2c6c5-136">Selecteer in het deelvenster resultaten hello, **Datahug**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2c6c5-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c6c5-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2c6c5-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Datahug op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2c6c5-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2c6c5-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Datahug is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="2c6c5-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Datahug toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="2c6c5-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Datahug.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="2c6c5-143">tooconfigure en eenmalige aanmelding Azure AD-test met Datahug, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2c6c5-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2c6c5-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2c6c5-146">**[Maken van een testgebruiker Datahug](#creating-a-datahug-test-user)**  -toohave een equivalent van Britta Simon in Datahug die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2c6c5-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2c6c5-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2c6c5-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2c6c5-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2c6c5-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Datahug configureren.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="2c6c5-151">**Azure AD tooconfigure eenmalige aanmelding met Datahug, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c6c5-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c6c5-152">In de Azure-portal op Hallo Hallo **Datahug** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2c6c5-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="2c6c5-156">Op Hallo **Datahug domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="2c6c5-158">a.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-158">a.</span></span> <span data-ttu-id="2c6c5-159">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="2c6c5-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="2c6c5-160">b.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-160">b.</span></span> <span data-ttu-id="2c6c5-161">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="2c6c5-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="2c6c5-162">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2c6c5-163">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="2c6c5-165">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="2c6c5-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2c6c5-166">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-166">These values are not hello real.</span></span> <span data-ttu-id="2c6c5-167">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="2c6c5-168">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="2c6c5-169">Neem contact op met [Datahug Client ondersteuningsteam](http://datahug.com/about/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="2c6c5-170">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="2c6c5-172">Controleer **'Weergeven geavanceerde instellingen voor het ondertekenen van certificaat'** en Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="2c6c5-174">a.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-174">a.</span></span> <span data-ttu-id="2c6c5-175">In **ondertekening optie**, selecteer **aanmelding SAML-verklaring**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="2c6c5-176">b.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-176">b.</span></span> <span data-ttu-id="2c6c5-177">In **ondertekening algoritme**, selecteer **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="2c6c5-178">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-178">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="2c6c5-180">Op Hallo **Datahug configuratie** sectie, klikt u op **configureren Datahug** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2c6c5-181">Kopiëren Hallo **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2c6c5-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="2c6c5-183">tooconfigure eenmalige aanmelding op **Datahug** zijde, moet u toosend Hallo gedownload **Metadata XML**, **SAML entiteit-ID** en **SAML Single Sign-On-Service URL** te[Datahug ondersteuning](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="2c6c5-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="2c6c5-184">Ze deze toepassing hello toohave SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2c6c5-185">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2c6c5-186">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2c6c5-187">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2c6c5-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2c6c5-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2c6c5-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="2c6c5-189">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2c6c5-191">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c6c5-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c6c5-192">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2c6c5-194">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2c6c5-196">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2c6c5-198">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c6c5-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2c6c5-200">a.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-200">a.</span></span> <span data-ttu-id="2c6c5-201">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2c6c5-202">b.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-202">b.</span></span> <span data-ttu-id="2c6c5-203">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2c6c5-204">c.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-204">c.</span></span> <span data-ttu-id="2c6c5-205">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2c6c5-206">d.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-206">d.</span></span> <span data-ttu-id="2c6c5-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="2c6c5-208">Een testgebruiker Datahug maken</span><span class="sxs-lookup"><span data-stu-id="2c6c5-208">Creating a Datahug test user</span></span>

<span data-ttu-id="2c6c5-209">Azure AD tooenable gebruikers toolog in tooDatahug, ze in Datahug moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="2c6c5-210">Datahug, inrichting wanneer een handmatige taak is.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="2c6c5-211">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c6c5-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c6c5-212">Aanmelden tooyour Datahug bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="2c6c5-213">Beweeg de muisaanwijzer over Hallo **tandwiel** in Hallo rechterbovenhoek en klik op **instellingen**</span><span class="sxs-lookup"><span data-stu-id="2c6c5-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="2c6c5-215">Kies **mensen** en klik op Hallo **gebruikers toevoegen** tabblad</span><span class="sxs-lookup"><span data-stu-id="2c6c5-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="2c6c5-217">Typ Hallo e-mailadres van Hallo persoon die u wilt dat toocreate de account die voor en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="2c6c5-219">U kunt registratie mail toouser verzenden door te selecteren **verzenden welkomstbericht** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="2c6c5-220">Als u een account voor Salesforce Hallo welkomstbericht niet verzenden.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2c6c5-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c6c5-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2c6c5-222">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDatahug toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2c6c5-224">**tooassign Britta Simon tooDatahug, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2c6c5-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="2c6c5-225">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2c6c5-227">Selecteer in de lijst met de toepassingen van Hallo **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-227">In hello applications list, select **Datahug**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="2c6c5-229">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2c6c5-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-231">Click **Add** button.</span></span> <span data-ttu-id="2c6c5-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2c6c5-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2c6c5-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2c6c5-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2c6c5-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2c6c5-237">Testing single sign-on</span></span>

<span data-ttu-id="2c6c5-238">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="2c6c5-239">Als u op Hallo Datahug tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Datahug toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c6c5-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="2c6c5-240">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="2c6c5-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2c6c5-241">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2c6c5-241">Additional resources</span></span>

* [<span data-ttu-id="2c6c5-242">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c6c5-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c6c5-243">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2c6c5-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

