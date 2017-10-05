---
title: 'Zelfstudie: Azure Active Directory-integratie met UserVoice | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en UserVoice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: fcfda1c2ecb162fb93b70574a18bd745b72ee4db
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="a66ba-103">Zelfstudie: Azure Active Directory-integratie met UserVoice</span><span class="sxs-lookup"><span data-stu-id="a66ba-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="a66ba-104">In deze zelfstudie leert u hoe UserVoice integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a66ba-104">In this tutorial, you learn how to integrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a66ba-105">UserVoice integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a66ba-105">Integrating UserVoice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a66ba-106">U kunt beheren in Azure AD die toegang tot UserVoice heeft.</span><span class="sxs-lookup"><span data-stu-id="a66ba-106">You can control in Azure AD who has access to UserVoice.</span></span>
- <span data-ttu-id="a66ba-107">U kunt uw gebruikers automatisch ophalen aangemeld bij UserVoice (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a66ba-107">You can enable your users to automatically get signed-on to UserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a66ba-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="a66ba-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a66ba-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a66ba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a66ba-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a66ba-110">Prerequisites</span></span>

<span data-ttu-id="a66ba-111">Voor het configureren van Azure AD-integratie met UserVoice, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a66ba-111">To configure Azure AD integration with UserVoice, you need the following items:</span></span>

- <span data-ttu-id="a66ba-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a66ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a66ba-113">Een UserVoice eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a66ba-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a66ba-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a66ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a66ba-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a66ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a66ba-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a66ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a66ba-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a66ba-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a66ba-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a66ba-118">Scenario description</span></span>
<span data-ttu-id="a66ba-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a66ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a66ba-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a66ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a66ba-121">UserVoice uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a66ba-121">Adding UserVoice from the gallery</span></span>
2. <span data-ttu-id="a66ba-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a66ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-the-gallery"></a><span data-ttu-id="a66ba-123">UserVoice uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a66ba-123">Adding UserVoice from the gallery</span></span>
<span data-ttu-id="a66ba-124">Voor het configureren van de integratie van UserVoice in Azure AD, moet u UserVoice uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a66ba-124">To configure the integration of UserVoice into Azure AD, you need to add UserVoice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a66ba-125">**Als u wilt toevoegen UserVoice uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a66ba-125">**To add UserVoice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a66ba-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a66ba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="a66ba-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a66ba-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="a66ba-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a66ba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="a66ba-133">Typ in het zoekvak **UserVoice**, selecteer **UserVoice** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a66ba-133">In the search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button to add the application.</span></span>

    ![UserVoice in de lijst met resultaten](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a66ba-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="a66ba-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a66ba-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met UserVoice op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a66ba-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a66ba-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in UserVoice is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a66ba-137">For single sign-on to work, Azure AD needs to know what the counterpart user in UserVoice is to a user in Azure AD.</span></span> <span data-ttu-id="a66ba-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante UserVoice-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a66ba-138">In other words, a link relationship between an Azure AD user and the related user in UserVoice needs to be established.</span></span>

<span data-ttu-id="a66ba-139">Wijs in UserVoice, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a66ba-139">In UserVoice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a66ba-140">Om te configureren en testen van Azure AD eenmalige aanmelding met UserVoice, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a66ba-140">To configure and test Azure AD single sign-on with UserVoice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a66ba-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a66ba-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a66ba-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a66ba-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a66ba-143">**[Maak een testgebruiker UserVoice](#create-a-uservoice-test-user)**  - UserVoice die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="a66ba-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - to have a counterpart of Britta Simon in UserVoice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a66ba-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a66ba-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a66ba-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a66ba-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a66ba-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a66ba-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a66ba-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw UserVoice-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a66ba-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="a66ba-148">**Voor het configureren van Azure AD eenmalige aanmelding met UserVoice, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a66ba-148">**To configure Azure AD single sign-on with UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="a66ba-149">In de Azure-portal op de **UserVoice** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-149">In the Azure portal, on the **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a66ba-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a66ba-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="a66ba-153">Op de **UserVoice domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a66ba-153">On the **UserVoice Domain and URLs** section, perform the following steps:</span></span>

    ![URL's voor UserVoice-domein en één aanmelding informatie](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="a66ba-155">a.</span><span class="sxs-lookup"><span data-stu-id="a66ba-155">a.</span></span> <span data-ttu-id="a66ba-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="a66ba-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="a66ba-157">b.</span><span class="sxs-lookup"><span data-stu-id="a66ba-157">b.</span></span> <span data-ttu-id="a66ba-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="a66ba-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a66ba-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a66ba-159">These values are not real.</span></span> <span data-ttu-id="a66ba-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="a66ba-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a66ba-161">Neem contact op met [UserVoice Client ondersteuningsteam](https://www.uservoice.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a66ba-161">Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values.</span></span>

4. <span data-ttu-id="a66ba-162">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="a66ba-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="a66ba-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a66ba-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a66ba-166">Op de **UserVoice configuratie** sectie, klikt u op **configureren UserVoice** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a66ba-166">On the **UserVoice Configuration** section, click **Configure UserVoice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a66ba-167">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a66ba-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![UserVoice-configuratie](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="a66ba-169">In een ander browservenster, meld u aan bij uw bedrijf UserVoice site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a66ba-169">In a different web browser window, log in to your UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="a66ba-170">Klik in de werkbalk bovenaan op **instellingen**, en selecteer vervolgens **webportal** in het menu.</span><span class="sxs-lookup"><span data-stu-id="a66ba-170">In the toolbar on the top, click **Settings**, and then select **Web portal** from the menu.</span></span>
   
    <span data-ttu-id="a66ba-171">![Sectie met App-zijde](./media/active-directory-saas-uservoice-tutorial/ic777519.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="a66ba-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="a66ba-172">Op de **webportal** tabblad, in de **gebruikersverificatie** sectie, klikt u op **bewerken** openen de **gebruikersverificatie bewerken** dialoogvenster pagina.</span><span class="sxs-lookup"><span data-stu-id="a66ba-172">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="a66ba-173">![Web-portal tabblad](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web-portal")</span><span class="sxs-lookup"><span data-stu-id="a66ba-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="a66ba-174">Op de **gebruikersverificatie bewerken** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a66ba-174">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="a66ba-175">![Verificatie van gebruikers bewerken](./media/active-directory-saas-uservoice-tutorial/ic777521.png "gebruikersverificatie bewerken")</span><span class="sxs-lookup"><span data-stu-id="a66ba-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="a66ba-176">a.</span><span class="sxs-lookup"><span data-stu-id="a66ba-176">a.</span></span> <span data-ttu-id="a66ba-177">Klik op **eenmalige aanmelding (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="a66ba-178">b.</span><span class="sxs-lookup"><span data-stu-id="a66ba-178">b.</span></span> <span data-ttu-id="a66ba-179">Plakken de **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **extern aanmelden SSO** textbox.</span><span class="sxs-lookup"><span data-stu-id="a66ba-179">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="a66ba-180">c.</span><span class="sxs-lookup"><span data-stu-id="a66ba-180">c.</span></span> <span data-ttu-id="a66ba-181">Plak de **Sign-Out URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **SSO externe Sign-Out textbox**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-181">Paste the **Sign-Out URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="a66ba-182">d.</span><span class="sxs-lookup"><span data-stu-id="a66ba-182">d.</span></span> <span data-ttu-id="a66ba-183">Plak de **vingerafdruk** waarde, die u hebt gekopieerd vanuit Azure-portal in de **huidige vingerafdruk van certificaat SHA1** textbox.</span><span class="sxs-lookup"><span data-stu-id="a66ba-183">Paste the **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="a66ba-184">e.</span><span class="sxs-lookup"><span data-stu-id="a66ba-184">e.</span></span> <span data-ttu-id="a66ba-185">Klik op **verificatie-instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="a66ba-186">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a66ba-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a66ba-187">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a66ba-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a66ba-188">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a66ba-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a66ba-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a66ba-189">Create an Azure AD test user</span></span>

<span data-ttu-id="a66ba-190">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a66ba-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="a66ba-192">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a66ba-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a66ba-193">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="a66ba-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a66ba-195">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a66ba-197">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a66ba-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a66ba-199">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a66ba-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a66ba-201">a.</span><span class="sxs-lookup"><span data-stu-id="a66ba-201">a.</span></span> <span data-ttu-id="a66ba-202">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a66ba-203">b.</span><span class="sxs-lookup"><span data-stu-id="a66ba-203">b.</span></span> <span data-ttu-id="a66ba-204">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a66ba-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a66ba-205">c.</span><span class="sxs-lookup"><span data-stu-id="a66ba-205">c.</span></span> <span data-ttu-id="a66ba-206">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="a66ba-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a66ba-207">d.</span><span class="sxs-lookup"><span data-stu-id="a66ba-207">d.</span></span> <span data-ttu-id="a66ba-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="a66ba-209">Maak een testgebruiker UserVoice</span><span class="sxs-lookup"><span data-stu-id="a66ba-209">Create a UserVoice test user</span></span>

<span data-ttu-id="a66ba-210">Om Azure AD-gebruikers zich aanmelden bij UserVoice, moeten ze worden ingericht in UserVoice.</span><span class="sxs-lookup"><span data-stu-id="a66ba-210">To enable Azure AD users to log in to UserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="a66ba-211">In het geval van UserVoice is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a66ba-211">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="a66ba-212">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a66ba-212">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="a66ba-213">Meld u aan bij uw **UserVoice** tenant.</span><span class="sxs-lookup"><span data-stu-id="a66ba-213">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="a66ba-214">Ga naar **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-214">Go to **Settings**.</span></span>
   
    <span data-ttu-id="a66ba-215">![Instellingen](./media/active-directory-saas-uservoice-tutorial/ic777811.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="a66ba-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="a66ba-216">Klik op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-216">Click **General**.</span></span>

4. <span data-ttu-id="a66ba-217">Klik op **Agents en machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="a66ba-218">![Agents en machtigingen](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents en machtigingen")</span><span class="sxs-lookup"><span data-stu-id="a66ba-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="a66ba-219">Klik op **toevoegen admins**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="a66ba-220">![Toevoegen van beheerders](./media/active-directory-saas-uservoice-tutorial/ic777813.png "admins toevoegen")</span><span class="sxs-lookup"><span data-stu-id="a66ba-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="a66ba-221">Op de **uitnodigen admins** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a66ba-221">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="a66ba-222">![Beheerders uitnodigen](./media/active-directory-saas-uservoice-tutorial/ic777814.png "admins uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="a66ba-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="a66ba-223">a.</span><span class="sxs-lookup"><span data-stu-id="a66ba-223">a.</span></span> <span data-ttu-id="a66ba-224">Typ in het tekstvak voor de e-mailberichten, het e-mailadres van het account dat u wilt inrichten, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-224">In the Emails textbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="a66ba-225">b.</span><span class="sxs-lookup"><span data-stu-id="a66ba-225">b.</span></span> <span data-ttu-id="a66ba-226">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="a66ba-227">U kunt andere UserVoice gebruiker account hulpmiddelen voor het maken of API's die is geleverd door UserVoice aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="a66ba-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a66ba-228">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="a66ba-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="a66ba-229">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan UserVoice.</span><span class="sxs-lookup"><span data-stu-id="a66ba-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserVoice.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="a66ba-231">**Britta Simon om aan te wijzen UserVoice, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a66ba-231">**To assign Britta Simon to UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="a66ba-232">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a66ba-234">Selecteer in de lijst met toepassingen **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-234">In the applications list, select **UserVoice**.</span></span>

    ![De UserVoice-koppeling in de lijst met toepassingen](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="a66ba-236">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a66ba-236">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="a66ba-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a66ba-238">Click **Add** button.</span></span> <span data-ttu-id="a66ba-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a66ba-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="a66ba-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a66ba-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a66ba-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a66ba-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a66ba-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a66ba-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a66ba-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a66ba-244">Test single sign-on</span></span>

<span data-ttu-id="a66ba-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a66ba-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a66ba-246">Als u op de tegel UserVoice in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw UserVoice-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a66ba-246">When you click the UserVoice tile in the Access Panel, you should get automatically signed-on to your UserVoice application.</span></span>
<span data-ttu-id="a66ba-247">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a66ba-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a66ba-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a66ba-248">Additional resources</span></span>

* [<span data-ttu-id="a66ba-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a66ba-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a66ba-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a66ba-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

