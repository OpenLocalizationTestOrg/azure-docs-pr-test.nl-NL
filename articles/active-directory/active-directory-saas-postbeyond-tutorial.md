---
title: 'Zelfstudie: Azure Active Directory-integratie met PostBeyond | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en PostBeyond.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 80b920dc99619795cbc86e8cb2e3ac2a78a71932
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="618b1-103">Zelfstudie: Azure Active Directory-integratie met PostBeyond</span><span class="sxs-lookup"><span data-stu-id="618b1-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="618b1-104">In deze zelfstudie leert u hoe PostBeyond integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="618b1-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="618b1-105">PostBeyond integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="618b1-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="618b1-106">U kunt beheren in Azure AD die toegang tot PostBeyond heeft</span><span class="sxs-lookup"><span data-stu-id="618b1-106">You can control in Azure AD who has access to PostBeyond</span></span>
- <span data-ttu-id="618b1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij PostBeyond (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="618b1-107">You can enable your users to automatically get signed-on to PostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="618b1-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="618b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="618b1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="618b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="618b1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="618b1-110">Prerequisites</span></span>

<span data-ttu-id="618b1-111">Voor het configureren van Azure AD-integratie met PostBeyond, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="618b1-111">To configure Azure AD integration with PostBeyond, you need the following items:</span></span>

- <span data-ttu-id="618b1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="618b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="618b1-113">Een PostBeyond eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="618b1-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="618b1-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="618b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="618b1-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="618b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="618b1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="618b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="618b1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="618b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="618b1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="618b1-118">Scenario description</span></span>
<span data-ttu-id="618b1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="618b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="618b1-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="618b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="618b1-121">PostBeyond uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="618b1-121">Adding PostBeyond from the gallery</span></span>
2. <span data-ttu-id="618b1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="618b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-the-gallery"></a><span data-ttu-id="618b1-123">PostBeyond uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="618b1-123">Adding PostBeyond from the gallery</span></span>
<span data-ttu-id="618b1-124">Voor het configureren van de integratie van PostBeyond met Azure AD, moet u PostBeyond uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="618b1-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="618b1-125">**Als u wilt toevoegen PostBeyond uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="618b1-125">**To add PostBeyond from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="618b1-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="618b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="618b1-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="618b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="618b1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="618b1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="618b1-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="618b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="618b1-133">Typ in het zoekvak **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="618b1-133">In the search box, type **PostBeyond**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="618b1-135">Selecteer in het deelvenster resultaten **PostBeyond**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="618b1-135">In the results panel, select **PostBeyond**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="618b1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="618b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="618b1-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met PostBeyond op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="618b1-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="618b1-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in PostBeyond is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="618b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span></span> <span data-ttu-id="618b1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in PostBeyond tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="618b1-140">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span></span>

<span data-ttu-id="618b1-141">Wijs in PostBeyond, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="618b1-141">In PostBeyond, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="618b1-142">Om te configureren en testen van Azure AD eenmalige aanmelding met PostBeyond, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="618b1-142">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="618b1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="618b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="618b1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="618b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="618b1-145">**[Maken van een PostBeyond testgebruiker](#creating-a-postbeyond-test-user)**  - PostBeyond die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="618b1-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="618b1-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="618b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="618b1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="618b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="618b1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="618b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="618b1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing PostBeyond configureren.</span><span class="sxs-lookup"><span data-stu-id="618b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="618b1-150">**Voor het configureren van Azure AD eenmalige aanmelding met PostBeyond, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="618b1-150">**To configure Azure AD single sign-on with PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="618b1-151">In de Azure-portal op de **PostBeyond** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="618b1-151">In the Azure portal, on the **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="618b1-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="618b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="618b1-155">Op de **PostBeyond domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="618b1-155">On the **PostBeyond Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="618b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="618b1-157">a.</span></span> <span data-ttu-id="618b1-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="618b1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="618b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="618b1-159">b.</span></span> <span data-ttu-id="618b1-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="618b1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="618b1-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="618b1-161">These values are not real.</span></span> <span data-ttu-id="618b1-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="618b1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="618b1-163">Neem contact op met [PostBeyond Client ondersteuningsteam](mailto:sso@postbeyond.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="618b1-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) to get these values.</span></span> 
 
4. <span data-ttu-id="618b1-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="618b1-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="618b1-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="618b1-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="618b1-168">Op de **PostBeyond configuratie** sectie, klikt u op **configureren PostBeyond** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="618b1-168">On the **PostBeyond Configuration** section, click **Configure PostBeyond** to open **Configure sign-on** window.</span></span> <span data-ttu-id="618b1-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="618b1-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="618b1-171">Eenmalige aanmelding configureren op **PostBeyond** zijde, moet u de gedownloade verzenden **Certificate(Base64)**, **SAML entiteit-ID**, **SAML Single Sign-On Service-URL** en **Sign-Out URL** naar [PostBeyond ondersteuningsteam](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="618b1-171">To configure single sign-on on **PostBeyond** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** to [PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="618b1-172">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="618b1-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="618b1-173">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="618b1-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="618b1-174">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="618b1-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="618b1-175">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="618b1-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="618b1-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="618b1-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="618b1-177">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="618b1-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="618b1-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="618b1-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="618b1-180">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="618b1-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="618b1-182">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="618b1-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="618b1-184">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="618b1-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="618b1-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="618b1-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="618b1-188">a.</span><span class="sxs-lookup"><span data-stu-id="618b1-188">a.</span></span> <span data-ttu-id="618b1-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="618b1-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="618b1-190">b.</span><span class="sxs-lookup"><span data-stu-id="618b1-190">b.</span></span> <span data-ttu-id="618b1-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="618b1-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="618b1-192">c.</span><span class="sxs-lookup"><span data-stu-id="618b1-192">c.</span></span> <span data-ttu-id="618b1-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="618b1-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="618b1-194">d.</span><span class="sxs-lookup"><span data-stu-id="618b1-194">d.</span></span> <span data-ttu-id="618b1-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="618b1-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="618b1-196">Een PostBeyond testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="618b1-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="618b1-197">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in PostBeyond maken.</span><span class="sxs-lookup"><span data-stu-id="618b1-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="618b1-198">Als u niet hoe Britta Simon toevoegen in PostBeyond weet, neem contact op met [PostBeyond ondersteuningsteam](mailto:sso@postbeyond.com) toe te voegen van de testgebruiker en eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="618b1-198">If you don't know how to add Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="618b1-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="618b1-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="618b1-200">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="618b1-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PostBeyond.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="618b1-202">**Britta Simon om aan te wijzen PostBeyond, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="618b1-202">**To assign Britta Simon to PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="618b1-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="618b1-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="618b1-205">Selecteer in de lijst met toepassingen **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="618b1-205">In the applications list, select **PostBeyond**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="618b1-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="618b1-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="618b1-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="618b1-209">Click **Add** button.</span></span> <span data-ttu-id="618b1-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="618b1-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="618b1-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="618b1-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="618b1-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="618b1-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="618b1-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="618b1-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="618b1-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="618b1-215">Testing single sign-on</span></span>

<span data-ttu-id="618b1-216">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="618b1-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="618b1-217">Wanneer u klikt op de tegel PostBeyond in het deelvenster toegang krijgt u naar de PostBeyond aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="618b1-217">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span></span> <span data-ttu-id="618b1-218">Klik op **aanmelden met Office 365**, Voer uw Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="618b1-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="618b1-219">Vervolgens, u moet zijn aangemeld bij PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="618b1-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="618b1-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="618b1-220">Additional resources</span></span>

* [<span data-ttu-id="618b1-221">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="618b1-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="618b1-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="618b1-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

