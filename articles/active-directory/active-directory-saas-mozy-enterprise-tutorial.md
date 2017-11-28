---
title: 'Zelfstudie: Azure Active Directory-integratie met Mozy Enterprise | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Mozy Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="bbb59-103">Zelfstudie: Azure Active Directory-integratie met Mozy voor ondernemingen</span><span class="sxs-lookup"><span data-stu-id="bbb59-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="bbb59-104">In deze zelfstudie leert u hoe Mozy-onderneming integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbb59-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbb59-105">Mozy-onderneming integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bbb59-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbb59-106">U kunt beheren in Azure AD die toegang tot Mozy Enterprise heeft</span><span class="sxs-lookup"><span data-stu-id="bbb59-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="bbb59-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Mozy Enterprise (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="bbb59-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbb59-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bbb59-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bbb59-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbb59-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbb59-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bbb59-110">Prerequisites</span></span>

<span data-ttu-id="bbb59-111">Voor het configureren van Azure AD-integratie met Mozy voor ondernemingen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="bbb59-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="bbb59-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bbb59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbb59-113">Een Mozy Enterprise eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bbb59-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbb59-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bbb59-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbb59-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bbb59-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbb59-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bbb59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbb59-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbb59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbb59-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bbb59-118">Scenario description</span></span>
<span data-ttu-id="bbb59-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bbb59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbb59-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bbb59-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbb59-121">Mozy Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bbb59-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="bbb59-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bbb59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="bbb59-123">Mozy Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bbb59-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="bbb59-124">Voor het configureren van de integratie van Mozy Enterprise in Azure AD, moet u Mozy Enterprise uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bbb59-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbb59-125">**Als u wilt toevoegen Mozy Enterprise uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbb59-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbb59-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bbb59-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bbb59-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbb59-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bbb59-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbb59-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bbb59-133">Typ in het zoekvak **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="bbb59-135">Selecteer in het deelvenster resultaten **Mozy Enterprise**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="bbb59-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bbb59-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bbb59-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bbb59-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Mozy ondernemingen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="bbb59-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bbb59-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de onderneming Mozy is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbb59-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="bbb59-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de onderneming Mozy tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="bbb59-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="bbb59-141">In de onderneming Mozy, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="bbb59-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bbb59-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Mozy voor ondernemingen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="bbb59-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbb59-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bbb59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bbb59-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbb59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbb59-145">**[Maken van een testgebruiker Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  - Mozy Enterprise die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="bbb59-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbb59-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bbb59-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbb59-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bbb59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bbb59-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bbb59-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bbb59-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bbb59-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="bbb59-150">**Voor het configureren van Azure AD eenmalige aanmelding met Mozy voor ondernemingen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbb59-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="bbb59-151">In de Azure-portal op de **Mozy Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bbb59-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bbb59-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="bbb59-155">Op de **Mozy Enterprise domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bbb59-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="bbb59-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="bbb59-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bbb59-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="bbb59-158">This value is not real.</span></span> <span data-ttu-id="bbb59-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bbb59-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="bbb59-160">Neem contact op met [Mozy Enterprise Client ondersteuningsteam](http://support.mozy.com/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="bbb59-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="bbb59-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bbb59-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="bbb59-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bbb59-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bbb59-165">Op de **Mozy Ondernemingsconfiguratie** sectie, klikt u op **configureren Mozy Enterprise** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bbb59-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bbb59-166">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bbb59-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="bbb59-168">In een ander browservenster, meld u bij uw bedrijf Mozy Enterprise site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bbb59-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="bbb59-169">In de **configuratie** sectie, klikt u op **verificatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="bbb59-170">![Verificatiebeleid](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "verificatiebeleid")</span><span class="sxs-lookup"><span data-stu-id="bbb59-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="bbb59-171">Op de **verificatiebeleid** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bbb59-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="bbb59-172">![Verificatiebeleid](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "verificatiebeleid")</span><span class="sxs-lookup"><span data-stu-id="bbb59-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="bbb59-173">a.</span><span class="sxs-lookup"><span data-stu-id="bbb59-173">a.</span></span> <span data-ttu-id="bbb59-174">Selecteer **adreslijstservice** als **Provider**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="bbb59-175">b.</span><span class="sxs-lookup"><span data-stu-id="bbb59-175">b.</span></span> <span data-ttu-id="bbb59-176">Selecteer **Gebruik LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="bbb59-177">c.</span><span class="sxs-lookup"><span data-stu-id="bbb59-177">c.</span></span> <span data-ttu-id="bbb59-178">Klik op de **SAML-verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="bbb59-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="bbb59-179">d.</span><span class="sxs-lookup"><span data-stu-id="bbb59-179">d.</span></span> <span data-ttu-id="bbb59-180">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit de Azure-portal in de **-URL voor webverificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="bbb59-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="bbb59-181">e.</span><span class="sxs-lookup"><span data-stu-id="bbb59-181">e.</span></span> <span data-ttu-id="bbb59-182">Plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit de Azure-portal in de **SAML-eindpunt** textbox.</span><span class="sxs-lookup"><span data-stu-id="bbb59-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="bbb59-183">f.</span><span class="sxs-lookup"><span data-stu-id="bbb59-183">f.</span></span> <span data-ttu-id="bbb59-184">Open uw gedownloade base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plak het gehele certificaat in **SAML certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="bbb59-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="bbb59-185">g.</span><span class="sxs-lookup"><span data-stu-id="bbb59-185">g.</span></span> <span data-ttu-id="bbb59-186">Selecteer **eenmalige aanmelding inschakelen voor beheerders aanmelden met hun netwerkreferenties**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="bbb59-187">h.</span><span class="sxs-lookup"><span data-stu-id="bbb59-187">h.</span></span> <span data-ttu-id="bbb59-188">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="bbb59-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="bbb59-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bbb59-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="bbb59-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bbb59-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbb59-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bbb59-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bbb59-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="bbb59-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bbb59-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bbb59-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbb59-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbb59-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bbb59-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbb59-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbb59-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbb59-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbb59-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bbb59-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbb59-204">a.</span><span class="sxs-lookup"><span data-stu-id="bbb59-204">a.</span></span> <span data-ttu-id="bbb59-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbb59-206">b.</span><span class="sxs-lookup"><span data-stu-id="bbb59-206">b.</span></span> <span data-ttu-id="bbb59-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbb59-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbb59-208">c.</span><span class="sxs-lookup"><span data-stu-id="bbb59-208">c.</span></span> <span data-ttu-id="bbb59-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bbb59-210">d.</span><span class="sxs-lookup"><span data-stu-id="bbb59-210">d.</span></span> <span data-ttu-id="bbb59-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="bbb59-212">Maken van een testgebruiker Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="bbb59-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="bbb59-213">Om in te schakelen gebruikers van Azure AD aan te melden bij Mozy Enterprise, moeten ze worden ingericht in Mozy-onderneming.</span><span class="sxs-lookup"><span data-stu-id="bbb59-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="bbb59-214">In het geval van Mozy Enterprise is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="bbb59-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="bbb59-215">U kunt andere Mozy Enterprise gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Mozy Enterprise aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="bbb59-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="bbb59-216">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbb59-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="bbb59-217">Meld u aan bij uw **Mozy Enterprise** tenant.</span><span class="sxs-lookup"><span data-stu-id="bbb59-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="bbb59-218">Klik op **gebruikers**, en klik vervolgens op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="bbb59-219">![Gebruikers](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="bbb59-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="bbb59-220">De **nieuwe gebruiker toevoegen** optie wordt alleen weergegeven als **Mozy** is geselecteerd als de provider onder **verificatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="bbb59-221">Als SAML-verificatie is geconfigureerd, worden klikt u vervolgens de gebruikers automatisch toegevoegd op de eerste aanmelding via eenmalige aanmelding op.</span><span class="sxs-lookup"><span data-stu-id="bbb59-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="bbb59-222">In het gebruikersdialoogvenster nieuwe de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bbb59-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="bbb59-223">![Gebruikers toevoegen](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="bbb59-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="bbb59-224">a.</span><span class="sxs-lookup"><span data-stu-id="bbb59-224">a.</span></span> <span data-ttu-id="bbb59-225">Van de **kiest u een groep** , selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="bbb59-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="bbb59-226">b.</span><span class="sxs-lookup"><span data-stu-id="bbb59-226">b.</span></span> <span data-ttu-id="bbb59-227">Van de **wat voor soort gebruiker** , selecteert u een type.</span><span class="sxs-lookup"><span data-stu-id="bbb59-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="bbb59-228">c.</span><span class="sxs-lookup"><span data-stu-id="bbb59-228">c.</span></span> <span data-ttu-id="bbb59-229">In de **gebruikersnaam** textbox, typ de naam van de Azure AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bbb59-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="bbb59-230">d.</span><span class="sxs-lookup"><span data-stu-id="bbb59-230">d.</span></span> <span data-ttu-id="bbb59-231">In de **e** textbox, typ de e-mailadres van de Azure AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bbb59-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="bbb59-232">e.</span><span class="sxs-lookup"><span data-stu-id="bbb59-232">e.</span></span> <span data-ttu-id="bbb59-233">Selecteer **gebruiker instructie e-mail verzenden**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="bbb59-234">f.</span><span class="sxs-lookup"><span data-stu-id="bbb59-234">f.</span></span> <span data-ttu-id="bbb59-235">Klik op **toevoegen van gebruiker (s)**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="bbb59-236">Nadat de gebruiker is gemaakt, wordt een e-mailbericht worden verzonden naar de Azure AD-gebruiker die een koppeling naar het account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="bbb59-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bbb59-237">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbb59-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bbb59-238">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding toegang verleent tot Mozy onderneming gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bbb59-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bbb59-240">**Britta Simon om aan te wijzen Mozy Enterprise, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbb59-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="bbb59-241">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bbb59-243">Selecteer in de lijst met toepassingen **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="bbb59-245">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bbb59-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bbb59-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bbb59-247">Click **Add** button.</span></span> <span data-ttu-id="bbb59-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbb59-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bbb59-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="bbb59-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bbb59-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbb59-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbb59-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbb59-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bbb59-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bbb59-253">Testing single sign-on</span></span>

<span data-ttu-id="bbb59-254">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bbb59-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bbb59-255">Wanneer u op de tegel Mozy Enterprise in het deelvenster toegang, moet u de aanmeldingspagina Mozy bedrijfstoepassing ophalen.</span><span class="sxs-lookup"><span data-stu-id="bbb59-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="bbb59-256">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbb59-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bbb59-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bbb59-257">Additional resources</span></span>

* [<span data-ttu-id="bbb59-258">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbb59-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbb59-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbb59-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

