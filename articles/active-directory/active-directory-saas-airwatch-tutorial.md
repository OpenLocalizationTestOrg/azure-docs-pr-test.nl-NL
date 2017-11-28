---
title: 'Zelfstudie: Azure Active Directory-integratie met AirWatch | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="bd897-103">Zelfstudie: Azure Active Directory-integratie met AirWatch</span><span class="sxs-lookup"><span data-stu-id="bd897-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="bd897-104">In deze zelfstudie leert u hoe toointegrate AirWatch met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd897-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd897-105">AirWatch integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bd897-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd897-106">U kunt beheren in Azure AD die tooAirWatch toegang heeft</span><span class="sxs-lookup"><span data-stu-id="bd897-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="bd897-107">U kunt uw gebruikers tooautomatically get aangemelde tooAirWatch (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="bd897-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd897-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bd897-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd897-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd897-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd897-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bd897-110">Prerequisites</span></span>

<span data-ttu-id="bd897-111">Azure AD-integratie met AirWatch tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="bd897-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="bd897-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bd897-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd897-113">Een AirWatch eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bd897-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd897-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bd897-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd897-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bd897-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd897-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bd897-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd897-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd897-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd897-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bd897-118">Scenario description</span></span>
<span data-ttu-id="bd897-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bd897-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd897-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bd897-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd897-121">Het toevoegen van AirWatch van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bd897-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="bd897-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bd897-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="bd897-123">Het toevoegen van AirWatch van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="bd897-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="bd897-124">tooconfigure hello integratie van AirWatch in Azure AD, moet u tooadd AirWatch uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bd897-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd897-125">**tooadd AirWatch via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd897-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd897-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bd897-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd897-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bd897-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd897-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bd897-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bd897-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd897-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bd897-133">Typ in het zoekvak Hallo **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="bd897-133">In hello search box, type **AirWatch**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="bd897-135">Selecteer in het deelvenster resultaten hello, **AirWatch**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bd897-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd897-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bd897-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd897-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met AirWatch op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bd897-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bd897-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in AirWatch is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd897-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="bd897-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in AirWatch toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="bd897-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="bd897-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in AirWatch.</span><span class="sxs-lookup"><span data-stu-id="bd897-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="bd897-142">tooconfigure en eenmalige aanmelding Azure AD-test met AirWatch, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd897-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd897-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="bd897-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd897-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd897-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd897-145">**[Maken van een testgebruiker AirWatch](#creating-a-airwatch-test-user)**  -toohave een equivalent van Britta Simon in AirWatch die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bd897-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd897-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bd897-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd897-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bd897-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd897-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bd897-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd897-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing AirWatch configureren.</span><span class="sxs-lookup"><span data-stu-id="bd897-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="bd897-150">**Azure AD tooconfigure eenmalige aanmelding met AirWatch, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd897-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd897-151">In de Azure-portal op Hallo Hallo **AirWatch** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bd897-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bd897-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bd897-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="bd897-155">Op Hallo **AirWatch domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd897-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="bd897-157">a.</span><span class="sxs-lookup"><span data-stu-id="bd897-157">a.</span></span> <span data-ttu-id="bd897-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="bd897-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="bd897-159">b.</span><span class="sxs-lookup"><span data-stu-id="bd897-159">b.</span></span> <span data-ttu-id="bd897-160">In Hallo **id** textbox Hallo typewaarde als`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="bd897-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd897-161">Deze waarde is geen echte Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd897-161">This value is not hello real.</span></span> <span data-ttu-id="bd897-162">Deze waarde bijwerken met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="bd897-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="bd897-163">Neem contact op met [AirWatch Client ondersteuningsteam](http://www.air-watch.com/company/contact-us/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="bd897-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="bd897-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bd897-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="bd897-166">Op Hallo **AirWatch configuratie** sectie, klikt u op **configureren AirWatch** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bd897-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bd897-167">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bd897-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="bd897-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bd897-169">Click **Save** button.</span></span>

    <span data-ttu-id="bd897-170">![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="bd897-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="bd897-171">In een ander browservenster, meld u aan tooyour AirWatch bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="bd897-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="bd897-172">Klik in het Hallo navigatiedeelvenster links op **Accounts**, en klik vervolgens op **beheerders**.</span><span class="sxs-lookup"><span data-stu-id="bd897-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="bd897-173">![Beheerders](./media/active-directory-saas-airwatch-tutorial/ic791920.png "beheerders")</span><span class="sxs-lookup"><span data-stu-id="bd897-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="bd897-174">Vouw Hallo **instellingen** menu en klik vervolgens op **Directory Services**.</span><span class="sxs-lookup"><span data-stu-id="bd897-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="bd897-175">![Instellingen](./media/active-directory-saas-airwatch-tutorial/ic791921.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="bd897-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="bd897-176">Klik op Hallo **gebruiker** tabblad in Hallo **Base DN** textbox, typ de naam van uw domein en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bd897-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="bd897-177">![Gebruiker](./media/active-directory-saas-airwatch-tutorial/ic791922.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="bd897-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="bd897-178">Klik op Hallo **Server** tabblad.</span><span class="sxs-lookup"><span data-stu-id="bd897-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="bd897-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span><span class="sxs-lookup"><span data-stu-id="bd897-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="bd897-180">Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd897-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="bd897-181">![Uploaden](./media/active-directory-saas-airwatch-tutorial/ic791924.png "uploaden")</span><span class="sxs-lookup"><span data-stu-id="bd897-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="bd897-182">a.</span><span class="sxs-lookup"><span data-stu-id="bd897-182">a.</span></span> <span data-ttu-id="bd897-183">Als **maptype**, selecteer **geen**.</span><span class="sxs-lookup"><span data-stu-id="bd897-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="bd897-184">b.</span><span class="sxs-lookup"><span data-stu-id="bd897-184">b.</span></span> <span data-ttu-id="bd897-185">Selecteer **SAML gebruiken voor verificatie**.</span><span class="sxs-lookup"><span data-stu-id="bd897-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="bd897-186">c.</span><span class="sxs-lookup"><span data-stu-id="bd897-186">c.</span></span> <span data-ttu-id="bd897-187">tooupload Hallo gedownloade certificaat, klik op **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="bd897-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="bd897-188">In Hallo **aanvragen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd897-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="bd897-189">![Aanvraag](./media/active-directory-saas-airwatch-tutorial/ic791925.png "aanvragen")</span><span class="sxs-lookup"><span data-stu-id="bd897-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="bd897-190">a.</span><span class="sxs-lookup"><span data-stu-id="bd897-190">a.</span></span> <span data-ttu-id="bd897-191">Als **Binding aanvraagtype**, selecteer **POST**.</span><span class="sxs-lookup"><span data-stu-id="bd897-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="bd897-192">b.</span><span class="sxs-lookup"><span data-stu-id="bd897-192">b.</span></span> <span data-ttu-id="bd897-193">In de Azure-portal op Hallo Hallo **op Airwatch eenmalige aanmelding configureren** dialoogvenster pagina, kopie Hallo **SAML Single Sign-On Service-URL** waarde en plak deze in Hallo **id-Provider Eenmalige aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="bd897-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="bd897-194">c.</span><span class="sxs-lookup"><span data-stu-id="bd897-194">c.</span></span> <span data-ttu-id="bd897-195">Als **NameID indeling**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="bd897-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="bd897-196">d.</span><span class="sxs-lookup"><span data-stu-id="bd897-196">d.</span></span> <span data-ttu-id="bd897-197">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bd897-197">Click **Save**.</span></span>

14. <span data-ttu-id="bd897-198">Klik op Hallo **gebruiker** tabblad opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bd897-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="bd897-199">![Gebruiker](./media/active-directory-saas-airwatch-tutorial/ic791926.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="bd897-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="bd897-200">In Hallo **kenmerk** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd897-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="bd897-201">![Kenmerk](./media/active-directory-saas-airwatch-tutorial/ic791927.png "kenmerk")</span><span class="sxs-lookup"><span data-stu-id="bd897-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="bd897-202">a.</span><span class="sxs-lookup"><span data-stu-id="bd897-202">a.</span></span> <span data-ttu-id="bd897-203">In Hallo **Object-id** textbox type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="bd897-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="bd897-204">b.</span><span class="sxs-lookup"><span data-stu-id="bd897-204">b.</span></span> <span data-ttu-id="bd897-205">In Hallo **gebruikersnaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="bd897-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="bd897-206">c.</span><span class="sxs-lookup"><span data-stu-id="bd897-206">c.</span></span> <span data-ttu-id="bd897-207">In Hallo **weergavenaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="bd897-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="bd897-208">d.</span><span class="sxs-lookup"><span data-stu-id="bd897-208">d.</span></span> <span data-ttu-id="bd897-209">In Hallo **voornaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="bd897-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="bd897-210">e.</span><span class="sxs-lookup"><span data-stu-id="bd897-210">e.</span></span> <span data-ttu-id="bd897-211">In Hallo **achternaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="bd897-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="bd897-212">f.</span><span class="sxs-lookup"><span data-stu-id="bd897-212">f.</span></span> <span data-ttu-id="bd897-213">In Hallo **e** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="bd897-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="bd897-214">g.</span><span class="sxs-lookup"><span data-stu-id="bd897-214">g.</span></span> <span data-ttu-id="bd897-215">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bd897-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd897-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bd897-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd897-217">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bd897-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bd897-219">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd897-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd897-220">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bd897-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd897-222">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bd897-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd897-224">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="bd897-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd897-226">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="bd897-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd897-228">a.</span><span class="sxs-lookup"><span data-stu-id="bd897-228">a.</span></span> <span data-ttu-id="bd897-229">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd897-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd897-230">b.</span><span class="sxs-lookup"><span data-stu-id="bd897-230">b.</span></span> <span data-ttu-id="bd897-231">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd897-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bd897-232">c.</span><span class="sxs-lookup"><span data-stu-id="bd897-232">c.</span></span> <span data-ttu-id="bd897-233">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bd897-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd897-234">d.</span><span class="sxs-lookup"><span data-stu-id="bd897-234">d.</span></span> <span data-ttu-id="bd897-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bd897-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="bd897-236">Een testgebruiker AirWatch maken</span><span class="sxs-lookup"><span data-stu-id="bd897-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="bd897-237">Azure AD tooenable gebruikers toolog in tooAirWatch, ze in tooAirWatch moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="bd897-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="bd897-238">AirWatch, inrichting wanneer een handmatige taak is.</span><span class="sxs-lookup"><span data-stu-id="bd897-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="bd897-239">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd897-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd897-240">Meld u bij tooyour **AirWatch** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="bd897-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="bd897-241">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **Accounts**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bd897-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="bd897-242">![Gebruikers](./media/active-directory-saas-airwatch-tutorial/ic791929.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="bd897-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="bd897-243">In Hallo **gebruikers** menu, klikt u op **lijstweergave**, en klik vervolgens op **toevoegen \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bd897-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="bd897-244">![Gebruiker toevoegen](./media/active-directory-saas-airwatch-tutorial/ic791930.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bd897-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="bd897-245">Op Hallo **toevoegen / bewerken van de gebruiker** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="bd897-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="bd897-246">![Gebruiker toevoegen](./media/active-directory-saas-airwatch-tutorial/ic791931.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bd897-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="bd897-247">Type Hallo **gebruikersnaam**, **wachtwoord**, **wachtwoord bevestigen**, **voornaam**, **achternaam**,  **E-mailadres** van een geldig Azure Active Directory-account die u wilt dat tooprovision in Hallo tekstvakken gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="bd897-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="bd897-248">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bd897-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="bd897-249">U kunt andere AirWatch gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door AirWatch tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bd897-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd897-250">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd897-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd897-251">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAirWatch toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="bd897-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bd897-253">**tooassign Britta Simon tooAirWatch, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="bd897-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd897-254">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bd897-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bd897-256">Selecteer in de lijst met de toepassingen van Hallo **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="bd897-256">In hello applications list, select **AirWatch**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="bd897-258">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bd897-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bd897-260">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bd897-260">Click **Add** button.</span></span> <span data-ttu-id="bd897-261">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd897-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bd897-263">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd897-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd897-264">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd897-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd897-265">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bd897-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd897-266">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bd897-266">Testing single sign-on</span></span>

<span data-ttu-id="bd897-267">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bd897-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd897-268">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="bd897-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="bd897-269">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bd897-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bd897-270">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bd897-270">Additional resources</span></span>

* [<span data-ttu-id="bd897-271">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd897-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd897-272">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd897-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

