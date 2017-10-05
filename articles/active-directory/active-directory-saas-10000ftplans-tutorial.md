---
title: 'Zelfstudie: Azure Active Directory-integratie met 10.000 ft plannen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en 10.000 ft plannen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="df4ad-103">Zelfstudie: Azure Active Directory-integratie met 10.000 ft plannen</span><span class="sxs-lookup"><span data-stu-id="df4ad-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="df4ad-104">In deze zelfstudie leert u hoe 10.000 ft plannen integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df4ad-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df4ad-105">10.000 ft plannen integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="df4ad-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df4ad-106">U kunt beheren in Azure AD die toegang tot 10.000 ft plannen heeft</span><span class="sxs-lookup"><span data-stu-id="df4ad-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="df4ad-107">U kunt uw gebruikers automatisch ophalen aangemeld bij 10.000 ft plannen (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="df4ad-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df4ad-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="df4ad-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="df4ad-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df4ad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df4ad-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="df4ad-110">Prerequisites</span></span>

<span data-ttu-id="df4ad-111">Voor het configureren van Azure AD-integratie met 10.000 ft plannen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="df4ad-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="df4ad-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="df4ad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df4ad-113">Een 10.000 ft plannen voor eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="df4ad-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df4ad-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="df4ad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df4ad-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="df4ad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df4ad-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="df4ad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df4ad-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefabonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df4ad-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df4ad-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="df4ad-118">Scenario description</span></span>
<span data-ttu-id="df4ad-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="df4ad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df4ad-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="df4ad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df4ad-121">In de galerie toe te voegen 10.000 ft plannen</span><span class="sxs-lookup"><span data-stu-id="df4ad-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="df4ad-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="df4ad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="df4ad-123">In de galerie toe te voegen 10.000 ft plannen</span><span class="sxs-lookup"><span data-stu-id="df4ad-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="df4ad-124">Voor het configureren van de integratie van 10.000 ft plannen in Azure AD, moet u 10.000 ft's uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="df4ad-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df4ad-125">**Als u wilt toevoegen 10.000 ft plannen uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df4ad-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df4ad-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="df4ad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df4ad-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="df4ad-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="df4ad-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="df4ad-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="df4ad-133">Typ in het zoekvak **10.000 ft plannen**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="df4ad-135">Selecteer in het deelvenster resultaten **10.000 ft plannen**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="df4ad-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df4ad-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="df4ad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df4ad-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met 10.000 ft plannen op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="df4ad-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="df4ad-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in 10.000 ft plannen in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="df4ad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="df4ad-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in 10.000 ft plannen moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="df4ad-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="df4ad-141">Wijs in 10.000 ft plannen, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="df4ad-142">Om te configureren en testen van Azure AD eenmalige aanmelding met 10.000 ft plannen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="df4ad-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df4ad-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df4ad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df4ad-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df4ad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df4ad-145">**[Maken van een 10.000 ft plannen testgebruiker](#creating-a-10000ft-plans-test-user)**  - hebben een equivalent van Britta Simon in 10.000 ft plannen die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="df4ad-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="df4ad-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df4ad-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="df4ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df4ad-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="df4ad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df4ad-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing 10.000 ft-plannen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="df4ad-150">**Voor het configureren van Azure AD eenmalige aanmelding met 10.000 ft plannen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df4ad-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="df4ad-151">In de Azure-portal op de **10.000 ft plannen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="df4ad-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="df4ad-155">Op de **10.000 ft domein plannen en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df4ad-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="df4ad-157">a.</span><span class="sxs-lookup"><span data-stu-id="df4ad-157">a.</span></span> <span data-ttu-id="df4ad-158">In de **aanmeldings-URL** textbox, typ de URL:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="df4ad-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="df4ad-159">b.</span><span class="sxs-lookup"><span data-stu-id="df4ad-159">b.</span></span> <span data-ttu-id="df4ad-160">In de **id** textbox, typ de URL:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="df4ad-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df4ad-161">De waarde voor **id** verschilt hebt u een aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="df4ad-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="df4ad-162">Neem contact op met [10.000 ft plannen ondersteuningsteam](https://www.10000ft.com/plans/support) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="df4ad-163">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="df4ad-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="df4ad-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="df4ad-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="df4ad-167">Op de **10.000 ft configuratie plannen** sectie, klikt u op **10.000 ft's configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="df4ad-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="df4ad-168">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="df4ad-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="df4ad-170">Eenmalige aanmelding configureren op **10.000 ft plannen** zijde, moet u de gedownloade verzenden **Certificate(Raw), Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [10.000 ft Plannen ondersteuningsteam](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="df4ad-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="df4ad-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="df4ad-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="df4ad-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="df4ad-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="df4ad-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df4ad-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df4ad-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="df4ad-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="df4ad-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="df4ad-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df4ad-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df4ad-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="df4ad-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df4ad-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df4ad-182">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="df4ad-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df4ad-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df4ad-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df4ad-186">a.</span><span class="sxs-lookup"><span data-stu-id="df4ad-186">a.</span></span> <span data-ttu-id="df4ad-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df4ad-188">b.</span><span class="sxs-lookup"><span data-stu-id="df4ad-188">b.</span></span> <span data-ttu-id="df4ad-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df4ad-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df4ad-190">c.</span><span class="sxs-lookup"><span data-stu-id="df4ad-190">c.</span></span> <span data-ttu-id="df4ad-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="df4ad-192">d.</span><span class="sxs-lookup"><span data-stu-id="df4ad-192">d.</span></span> <span data-ttu-id="df4ad-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="df4ad-194">Maken van een 10.000 ft testgebruiker plannen</span><span class="sxs-lookup"><span data-stu-id="df4ad-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="df4ad-195">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in 10.000 ft plannen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="df4ad-196">10.000 ft plannen ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="df4ad-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="df4ad-197">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="df4ad-197">There is no action item for you in this section.</span></span> <span data-ttu-id="df4ad-198">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot 10.000 ft plannen als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="df4ad-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="df4ad-199">Als u een gebruiker handmatig maken wilt, moet u contact op met de [10.000 ft plannen ondersteuningsteam](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="df4ad-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="df4ad-200">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="df4ad-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="df4ad-201">In deze sectie schakelt u Britta Simon gebruiken Azure eenmalige aanmelding toegang verleent tot 10.000 ft plannen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="df4ad-203">**Als u wilt toewijzen Britta Simon tot 10.000 ft plannen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="df4ad-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="df4ad-204">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="df4ad-206">Selecteer in de lijst met toepassingen **10.000 ft plannen**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="df4ad-208">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="df4ad-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="df4ad-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="df4ad-210">Click **Add** button.</span></span> <span data-ttu-id="df4ad-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="df4ad-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="df4ad-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="df4ad-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="df4ad-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="df4ad-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df4ad-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="df4ad-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="df4ad-216">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="df4ad-216">Testing single sign-on</span></span>

<span data-ttu-id="df4ad-217">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="df4ad-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="df4ad-218">Als u op de tegel 10.000 ft plannen in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing 10.000 ft-plannen.</span><span class="sxs-lookup"><span data-stu-id="df4ad-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="df4ad-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="df4ad-219">Additional resources</span></span>

* [<span data-ttu-id="df4ad-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df4ad-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df4ad-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df4ad-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

