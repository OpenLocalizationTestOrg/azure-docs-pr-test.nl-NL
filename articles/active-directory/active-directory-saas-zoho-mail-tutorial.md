---
title: 'Zelfstudie: Azure Active Directory-integratie met Zoho | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Zoho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="f9019-103">Zelfstudie: Azure Active Directory-integratie met Zoho</span><span class="sxs-lookup"><span data-stu-id="f9019-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="f9019-104">In deze zelfstudie leert u hoe Zoho integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9019-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9019-105">Zoho integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f9019-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9019-106">U kunt beheren in Azure AD die toegang tot Zoho heeft.</span><span class="sxs-lookup"><span data-stu-id="f9019-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="f9019-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Zoho (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f9019-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f9019-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="f9019-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f9019-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9019-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9019-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f9019-110">Prerequisites</span></span>

<span data-ttu-id="f9019-111">Voor het configureren van Azure AD-integratie met Zoho, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f9019-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="f9019-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f9019-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9019-113">Een Zoho eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f9019-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9019-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f9019-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9019-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f9019-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9019-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f9019-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9019-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9019-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9019-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f9019-118">Scenario description</span></span>
<span data-ttu-id="f9019-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f9019-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9019-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f9019-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9019-121">Zoho uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f9019-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="f9019-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f9019-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="f9019-123">Zoho uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f9019-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="f9019-124">Voor het configureren van de integratie van Zoho in Azure AD, moet u Zoho uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f9019-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9019-125">**Als u wilt toevoegen Zoho uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f9019-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9019-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f9019-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="f9019-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f9019-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9019-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f9019-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="f9019-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f9019-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="f9019-133">Typ in het zoekvak **Zoho**, selecteer **Zoho** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f9019-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho in de lijst met resultaten](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f9019-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9019-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f9019-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Zoho op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f9019-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f9019-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Zoho is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9019-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="f9019-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Zoho tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f9019-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="f9019-139">Wijs in Zoho, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f9019-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f9019-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Zoho, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f9019-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9019-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f9019-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9019-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9019-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9019-143">**[Maak een testgebruiker Zoho](#create-a-zoho-test-user)**  - Zoho die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f9019-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9019-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f9019-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9019-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f9019-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f9019-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f9019-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f9019-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Zoho configureren.</span><span class="sxs-lookup"><span data-stu-id="f9019-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="f9019-148">**Voor het configureren van Azure AD eenmalige aanmelding met Zoho, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f9019-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="f9019-149">In de Azure-portal op de **Zoho** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f9019-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f9019-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f9019-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="f9019-153">Op de **Zoho domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f9019-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en Zoho domein eenmalige aanmelding informatie](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="f9019-155">a.</span><span class="sxs-lookup"><span data-stu-id="f9019-155">a.</span></span> <span data-ttu-id="f9019-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="f9019-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9019-157">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f9019-157">This value is not real.</span></span> <span data-ttu-id="f9019-158">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f9019-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f9019-159">Neem contact op met [Zoho Client ondersteuningsteam](https://www.zoho.com/mail/contact.html) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="f9019-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="f9019-160">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f9019-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="f9019-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f9019-162">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f9019-164">Op de **Zoho configuratie** sectie, klikt u op **configureren Zoho** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f9019-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f9019-165">Kopieer de **Sign-Out-URL, de URL wachtwoord wijzigen en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f9019-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoho configuratie](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="f9019-167">In een ander browservenster, meld u bij uw bedrijf Zoho Mail site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f9019-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="f9019-168">Ga naar de **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="f9019-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="f9019-169">![Het Configuratiescherm](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Configuratiescherm")</span><span class="sxs-lookup"><span data-stu-id="f9019-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="f9019-170">Klik op de **SAML-verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f9019-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="f9019-171">![SAML-verificatie](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="f9019-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="f9019-172">In de **SAML verificatiegegevens** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f9019-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f9019-173">![Details van SAML-verificatie](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Details van SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="f9019-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="f9019-174">a.</span><span class="sxs-lookup"><span data-stu-id="f9019-174">a.</span></span> <span data-ttu-id="f9019-175">In de **aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f9019-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f9019-176">b.</span><span class="sxs-lookup"><span data-stu-id="f9019-176">b.</span></span> <span data-ttu-id="f9019-177">In de **afmelding URL** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f9019-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f9019-178">c.</span><span class="sxs-lookup"><span data-stu-id="f9019-178">c.</span></span> <span data-ttu-id="f9019-179">In de **URL van wijzigen wachtwoord** textbox plakken **URL van wijzigen wachtwoord** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f9019-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="f9019-180">d.</span><span class="sxs-lookup"><span data-stu-id="f9019-180">d.</span></span> <span data-ttu-id="f9019-181">Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **PublicKey** textbox.</span><span class="sxs-lookup"><span data-stu-id="f9019-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="f9019-182">e.</span><span class="sxs-lookup"><span data-stu-id="f9019-182">e.</span></span> <span data-ttu-id="f9019-183">Als **algoritme**, selecteer **RSA**.</span><span class="sxs-lookup"><span data-stu-id="f9019-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="f9019-184">f.</span><span class="sxs-lookup"><span data-stu-id="f9019-184">f.</span></span> <span data-ttu-id="f9019-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9019-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="f9019-186">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f9019-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9019-187">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f9019-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9019-188">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f9019-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f9019-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f9019-189">Create an Azure AD test user</span></span>

<span data-ttu-id="f9019-190">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f9019-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="f9019-192">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f9019-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9019-193">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="f9019-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f9019-195">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f9019-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f9019-197">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f9019-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f9019-199">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f9019-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f9019-201">a.</span><span class="sxs-lookup"><span data-stu-id="f9019-201">a.</span></span> <span data-ttu-id="f9019-202">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9019-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9019-203">b.</span><span class="sxs-lookup"><span data-stu-id="f9019-203">b.</span></span> <span data-ttu-id="f9019-204">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9019-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f9019-205">c.</span><span class="sxs-lookup"><span data-stu-id="f9019-205">c.</span></span> <span data-ttu-id="f9019-206">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="f9019-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f9019-207">d.</span><span class="sxs-lookup"><span data-stu-id="f9019-207">d.</span></span> <span data-ttu-id="f9019-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f9019-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="f9019-209">Een testgebruiker Zoho maken</span><span class="sxs-lookup"><span data-stu-id="f9019-209">Create a Zoho test user</span></span>

<span data-ttu-id="f9019-210">Om in te schakelen gebruikers van Azure AD aan te melden bij Zoho Mail, moeten ze worden ingericht in Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="f9019-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="f9019-211">In het geval van Zoho Mail is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="f9019-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="f9019-212">U kunt andere Zoho afdruk gebruiker account hulpmiddelen voor het maken of API's geleverd door Zoho E-mail aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="f9019-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="f9019-213">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f9019-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="f9019-214">Meld u aan bij uw **Zoho Mail** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f9019-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="f9019-215">Ga naar **Configuratiescherm \> e & Docs**.</span><span class="sxs-lookup"><span data-stu-id="f9019-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="f9019-216">Ga naar **Gebruikersdetails \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f9019-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="f9019-217">![Gebruiker toevoegen](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="f9019-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="f9019-218">Op de **gebruikers toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f9019-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="f9019-219">![Gebruiker toevoegen](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="f9019-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="f9019-220">a.</span><span class="sxs-lookup"><span data-stu-id="f9019-220">a.</span></span> <span data-ttu-id="f9019-221">In de **voornaam** textbox type de voornaam van de gebruiker, zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f9019-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="f9019-222">b.</span><span class="sxs-lookup"><span data-stu-id="f9019-222">b.</span></span> <span data-ttu-id="f9019-223">In de **achternaam** textbox type de naam van de laatste gebruiker, zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f9019-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="f9019-224">c.</span><span class="sxs-lookup"><span data-stu-id="f9019-224">c.</span></span> <span data-ttu-id="f9019-225">In de **E-mail-ID** textbox type de e-mail-id van gebruiker, zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f9019-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f9019-226">d.</span><span class="sxs-lookup"><span data-stu-id="f9019-226">d.</span></span> <span data-ttu-id="f9019-227">In de **wachtwoord** textbox, voer het wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f9019-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="f9019-228">e.</span><span class="sxs-lookup"><span data-stu-id="f9019-228">e.</span></span> <span data-ttu-id="f9019-229">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9019-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="f9019-230">De houder van Azure Active Directory-account ontvangt een e-mailbericht met een koppeling naar het account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="f9019-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f9019-231">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="f9019-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="f9019-232">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Zoho.</span><span class="sxs-lookup"><span data-stu-id="f9019-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="f9019-234">**Britta Simon om aan te wijzen Zoho, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f9019-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="f9019-235">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f9019-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f9019-237">Selecteer in de lijst met toepassingen **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="f9019-237">In the applications list, select **Zoho**.</span></span>

    ![De koppeling Zoho in de lijst met toepassingen](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="f9019-239">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f9019-239">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="f9019-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f9019-241">Click **Add** button.</span></span> <span data-ttu-id="f9019-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f9019-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="f9019-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f9019-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9019-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f9019-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9019-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f9019-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f9019-247">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f9019-247">Test single sign-on</span></span>

<span data-ttu-id="f9019-248">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f9019-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f9019-249">Als u op de tegel Zoho in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Zoho.</span><span class="sxs-lookup"><span data-stu-id="f9019-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="f9019-250">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9019-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f9019-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f9019-251">Additional resources</span></span>

* [<span data-ttu-id="f9019-252">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9019-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9019-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f9019-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

