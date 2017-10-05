---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix ShareFile | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Citrix ShareFile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="c59c7-103">Zelfstudie: Azure Active Directory-integratie met Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="c59c7-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="c59c7-104">In deze zelfstudie leert u hoe Citrix ShareFile integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c59c7-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c59c7-105">Citrix ShareFile integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c59c7-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c59c7-106">U kunt beheren in Azure AD die toegang tot Citrix ShareFile heeft.</span><span class="sxs-lookup"><span data-stu-id="c59c7-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="c59c7-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Citrix ShareFile (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="c59c7-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c59c7-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="c59c7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c59c7-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c59c7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c59c7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c59c7-110">Prerequisites</span></span>

<span data-ttu-id="c59c7-111">Voor het configureren van Azure AD-integratie met Citrix ShareFile, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c59c7-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="c59c7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c59c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c59c7-113">Een Citrix ShareFile eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c59c7-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c59c7-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c59c7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c59c7-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c59c7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c59c7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c59c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c59c7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c59c7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c59c7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c59c7-118">Scenario description</span></span>
<span data-ttu-id="c59c7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c59c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c59c7-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c59c7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c59c7-121">Citrix ShareFile uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c59c7-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="c59c7-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="c59c7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="c59c7-123">Citrix ShareFile uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c59c7-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="c59c7-124">Voor het configureren van de integratie van Citrix ShareFile in Azure AD, moet u Citrix ShareFile uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c59c7-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c59c7-125">**Als u wilt toevoegen Citrix ShareFile uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c59c7-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c59c7-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c59c7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="c59c7-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c59c7-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="c59c7-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c59c7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="c59c7-133">Typ in het zoekvak **Citrix ShareFile**, selecteer **Citrix ShareFile** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c59c7-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Citrix ShareFile in de lijst met resultaten](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c59c7-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="c59c7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c59c7-136">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Citrix ShareFile op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c59c7-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c59c7-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Citrix ShareFile is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c59c7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="c59c7-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Citrix ShareFile tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c59c7-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="c59c7-139">Wijs in Citrix ShareFile, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c59c7-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c59c7-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Citrix ShareFile, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c59c7-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c59c7-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c59c7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c59c7-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c59c7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c59c7-143">**[Maak een testgebruiker Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  - Citrix ShareFile die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c59c7-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c59c7-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c59c7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c59c7-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c59c7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c59c7-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c59c7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c59c7-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Citrix ShareFile configureren.</span><span class="sxs-lookup"><span data-stu-id="c59c7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="c59c7-148">**Voor het configureren van Azure AD eenmalige aanmelding met Citrix ShareFile, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c59c7-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="c59c7-149">In de Azure-portal op de **Citrix ShareFile** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c59c7-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c59c7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="c59c7-153">Op de **Citrix ShareFile domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c59c7-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Citrix ShareFile domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="c59c7-155">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="c59c7-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c59c7-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="c59c7-156">This value is not real.</span></span> <span data-ttu-id="c59c7-157">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c59c7-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c59c7-158">Neem contact op met [Citrix ShareFile Client ondersteuningsteam](https://www.citrix.co.in/products/sharefile/support.html) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="c59c7-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="c59c7-159">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c59c7-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="c59c7-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c59c7-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c59c7-163">Op de **Citrix-configuratie voor ShareFile** sectie, klikt u op **configureren Citrix ShareFile** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c59c7-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c59c7-164">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c59c7-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Citrix ShareFile-configuratie](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="c59c7-166">In een ander browservenster, meld u aan bij uw **Citrix ShareFile** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c59c7-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="c59c7-167">Klik in de werkbalk bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="c59c7-168">Selecteer in het navigatiedeelvenster links **configureren Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="c59c7-169">![Beheer account](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account beheer")</span><span class="sxs-lookup"><span data-stu-id="c59c7-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="c59c7-170">Op de **Single Sign-On / SAML 2.0-configuratie** dialoogvenster pagina onder **basisinstellingen**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c59c7-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="c59c7-171">![Eenmalige aanmelding](./media/active-directory-saas-sharefile-tutorial/ic773628.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="c59c7-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="c59c7-172">a.</span><span class="sxs-lookup"><span data-stu-id="c59c7-172">a.</span></span> <span data-ttu-id="c59c7-173">Klik op **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="c59c7-174">b.</span><span class="sxs-lookup"><span data-stu-id="c59c7-174">b.</span></span> <span data-ttu-id="c59c7-175">In **uw IDP verlener / entiteit-ID** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c59c7-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c59c7-176">c.</span><span class="sxs-lookup"><span data-stu-id="c59c7-176">c.</span></span> <span data-ttu-id="c59c7-177">Klik op **wijziging** naast de **X.509-certificaat** veld en upload het certificaat dat u hebt gedownload van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c59c7-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="c59c7-178">d.</span><span class="sxs-lookup"><span data-stu-id="c59c7-178">d.</span></span> <span data-ttu-id="c59c7-179">In **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c59c7-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c59c7-180">e.</span><span class="sxs-lookup"><span data-stu-id="c59c7-180">e.</span></span> <span data-ttu-id="c59c7-181">In **afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c59c7-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="c59c7-182">Klik op **opslaan** op de Citrix ShareFile-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="c59c7-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="c59c7-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c59c7-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c59c7-184">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c59c7-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c59c7-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c59c7-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c59c7-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c59c7-186">Create an Azure AD test user</span></span>

<span data-ttu-id="c59c7-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c59c7-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="c59c7-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c59c7-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c59c7-190">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="c59c7-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c59c7-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c59c7-194">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c59c7-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c59c7-196">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c59c7-196">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c59c7-198">a.</span><span class="sxs-lookup"><span data-stu-id="c59c7-198">a.</span></span> <span data-ttu-id="c59c7-199">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c59c7-200">b.</span><span class="sxs-lookup"><span data-stu-id="c59c7-200">b.</span></span> <span data-ttu-id="c59c7-201">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c59c7-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c59c7-202">c.</span><span class="sxs-lookup"><span data-stu-id="c59c7-202">c.</span></span> <span data-ttu-id="c59c7-203">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="c59c7-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c59c7-204">d.</span><span class="sxs-lookup"><span data-stu-id="c59c7-204">d.</span></span> <span data-ttu-id="c59c7-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="c59c7-206">Een testgebruiker Citrix ShareFile maken</span><span class="sxs-lookup"><span data-stu-id="c59c7-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="c59c7-207">Om in te schakelen gebruikers van Azure AD aan te melden bij Citrix ShareFile, moeten ze worden ingericht in Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="c59c7-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="c59c7-208">In het geval van Citrix ShareFile is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c59c7-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="c59c7-209">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c59c7-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c59c7-210">Meld u aan bij uw **Citrix ShareFile** tenant.</span><span class="sxs-lookup"><span data-stu-id="c59c7-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="c59c7-211">Klik op **gebruikers beheren \> beheren van gebruikers Home \> + werknemer**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="c59c7-212">![Maken van de werknemer](./media/active-directory-saas-sharefile-tutorial/IC781050.png "werknemer maken")</span><span class="sxs-lookup"><span data-stu-id="c59c7-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="c59c7-213">Op de **basisinformatie** sectie, voert u onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c59c7-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="c59c7-214">![Algemene informatie](./media/active-directory-saas-sharefile-tutorial/IC799951.png "basisinformatie")</span><span class="sxs-lookup"><span data-stu-id="c59c7-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="c59c7-215">a.</span><span class="sxs-lookup"><span data-stu-id="c59c7-215">a.</span></span> <span data-ttu-id="c59c7-216">In de **e-mailadres** textbox, typt u het e-mailadres Britta Simon als  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c59c7-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="c59c7-217">b.</span><span class="sxs-lookup"><span data-stu-id="c59c7-217">b.</span></span> <span data-ttu-id="c59c7-218">In de **voornaam** textbox type **voornaam** van gebruiker als **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="c59c7-219">c.</span><span class="sxs-lookup"><span data-stu-id="c59c7-219">c.</span></span> <span data-ttu-id="c59c7-220">In de **achternaam** textbox type **achternaam** van gebruiker als **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="c59c7-221">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="c59c7-222">De accounthouder Azure AD ontvangt dat een e-mailbericht en Ga als volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt. U kunt geen andere hulpprogramma's voor Citrix ShareFile gebruiker-account maken of API's die worden geleverd door Citrix ShareFile gebruiken voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c59c7-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c59c7-223">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="c59c7-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="c59c7-224">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="c59c7-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="c59c7-226">**Britta Simon om aan te wijzen Citrix ShareFile, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c59c7-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="c59c7-227">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c59c7-229">Selecteer in de lijst met toepassingen **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![De Citrix ShareFile-koppeling in de lijst met toepassingen](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="c59c7-231">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c59c7-231">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="c59c7-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c59c7-233">Click **Add** button.</span></span> <span data-ttu-id="c59c7-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c59c7-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="c59c7-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c59c7-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c59c7-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c59c7-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c59c7-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c59c7-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c59c7-239">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c59c7-239">Test single sign-on</span></span>

<span data-ttu-id="c59c7-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c59c7-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c59c7-241">Als u op de tegel Citrix ShareFile in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="c59c7-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="c59c7-242">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c59c7-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c59c7-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c59c7-243">Additional resources</span></span>

* [<span data-ttu-id="c59c7-244">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c59c7-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c59c7-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c59c7-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

