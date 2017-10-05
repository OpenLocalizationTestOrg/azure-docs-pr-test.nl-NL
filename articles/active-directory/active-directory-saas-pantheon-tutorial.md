---
title: 'Zelfstudie: Azure Active Directory-integratie met Pantheon | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Pantheon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="04920-103">Zelfstudie: Azure Active Directory-integratie met Pantheon</span><span class="sxs-lookup"><span data-stu-id="04920-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="04920-104">In deze zelfstudie leert u hoe Pantheon integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="04920-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04920-105">Pantheon integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="04920-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="04920-106">U kunt beheren in Azure AD die toegang tot Pantheon heeft</span><span class="sxs-lookup"><span data-stu-id="04920-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="04920-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Pantheon (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="04920-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04920-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="04920-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="04920-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="04920-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04920-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="04920-110">Prerequisites</span></span>

<span data-ttu-id="04920-111">Voor het configureren van Azure AD-integratie met Pantheon, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="04920-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="04920-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="04920-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04920-113">Een Pantheon eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="04920-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04920-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="04920-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04920-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="04920-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04920-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="04920-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04920-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04920-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04920-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="04920-118">Scenario description</span></span>
<span data-ttu-id="04920-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="04920-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04920-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="04920-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04920-121">Pantheon uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="04920-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="04920-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="04920-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="04920-123">Pantheon uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="04920-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="04920-124">Voor het configureren van de integratie van Pantheon in Azure AD, moet u Pantheon uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="04920-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="04920-125">**Als u wilt toevoegen Pantheon uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="04920-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="04920-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="04920-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="04920-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="04920-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="04920-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="04920-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="04920-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04920-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="04920-133">Typ in het zoekvak **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="04920-133">In the search box, type **Pantheon**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="04920-135">Selecteer in het deelvenster resultaten **Pantheon**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="04920-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="04920-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="04920-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="04920-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Pantheon op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="04920-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="04920-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Pantheon is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04920-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="04920-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Pantheon tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="04920-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="04920-141">Wijs in Pantheon, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="04920-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="04920-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Pantheon, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="04920-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="04920-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="04920-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="04920-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04920-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04920-145">**[Maken van een testgebruiker Pantheon](#creating-a-pantheon-test-user)**  - Pantheon die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="04920-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="04920-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="04920-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04920-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="04920-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="04920-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="04920-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="04920-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Pantheon configureren.</span><span class="sxs-lookup"><span data-stu-id="04920-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="04920-150">**Voor het configureren van Azure AD eenmalige aanmelding met Pantheon, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="04920-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="04920-151">In de Azure-portal op de **Pantheon** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="04920-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="04920-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="04920-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="04920-155">Op de **Pantheon domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="04920-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="04920-157">a.</span><span class="sxs-lookup"><span data-stu-id="04920-157">a.</span></span> <span data-ttu-id="04920-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="04920-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="04920-159">b.</span><span class="sxs-lookup"><span data-stu-id="04920-159">b.</span></span> <span data-ttu-id="04920-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="04920-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="04920-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="04920-161">These values are not real.</span></span> <span data-ttu-id="04920-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="04920-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="04920-163">Neem contact op met [Pantheon ondersteuningsteam](https://pantheon.io/docs/getting-support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="04920-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

4. <span data-ttu-id="04920-164">De SAML-bevestiging verwacht pantheon toepassing in specifieke indeling die moet worden ingesteld van de kenmerkwaarde UserIdentifier met e-mailadres van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="04920-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="04920-165">Azure AD gebruikt standaard de UserPrincipalName voor UserIdentifier-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="04920-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="04920-166">Maar voor geslaagde integratie moet u deze waarde waarmee moet overeenkomen met de e-mailadres van de gebruiker aanpassen.</span><span class="sxs-lookup"><span data-stu-id="04920-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="04920-167">De integratie werkt alleen hierna moet u de juiste toewijzing.</span><span class="sxs-lookup"><span data-stu-id="04920-167">The integration will only work after doing the correct mapping.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="04920-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="04920-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="04920-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="04920-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="04920-173">Op de **Pantheon configuratie** sectie, klikt u op **configureren Pantheon** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="04920-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="04920-174">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="04920-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="04920-176">Eenmalige aanmelding configureren op **Pantheon** zijde, moet u de gedownloade verzenden **certificaat** en **SAML Single Sign-On Service-URL** naar [Pantheon ondersteuningsteam](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="04920-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="04920-177">U moet ook de e-mailbericht domein(en) informatie en de datum / tijd opgeven als u wilt dat deze verbinding.</span><span class="sxs-lookup"><span data-stu-id="04920-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="04920-178">U vindt meer informatie over het [hier](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="04920-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="04920-179">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="04920-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="04920-180">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="04920-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="04920-181">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04920-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="04920-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="04920-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="04920-183">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="04920-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="04920-185">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="04920-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="04920-186">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="04920-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04920-188">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="04920-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04920-190">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04920-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04920-192">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="04920-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04920-194">a.</span><span class="sxs-lookup"><span data-stu-id="04920-194">a.</span></span> <span data-ttu-id="04920-195">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="04920-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04920-196">b.</span><span class="sxs-lookup"><span data-stu-id="04920-196">b.</span></span> <span data-ttu-id="04920-197">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="04920-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04920-198">c.</span><span class="sxs-lookup"><span data-stu-id="04920-198">c.</span></span> <span data-ttu-id="04920-199">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="04920-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="04920-200">d.</span><span class="sxs-lookup"><span data-stu-id="04920-200">d.</span></span> <span data-ttu-id="04920-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="04920-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="04920-202">Een testgebruiker Pantheon maken</span><span class="sxs-lookup"><span data-stu-id="04920-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="04920-203">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Pantheon maken.</span><span class="sxs-lookup"><span data-stu-id="04920-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="04920-204">Volg de onderstaande stappen voor het toevoegen van de gebruiker in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="04920-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="04920-205">Moet eerst worden gemaakt in Pantheon voor eenmalige aanmelding gebruiker werken.</span><span class="sxs-lookup"><span data-stu-id="04920-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="04920-206">Aanmelden bij Pantheon met beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="04920-206">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="04920-207">Navigeer naar **organisatie** dashboardpagina.</span><span class="sxs-lookup"><span data-stu-id="04920-207">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="04920-208">Klik op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="04920-208">Click **People**.</span></span>

4. <span data-ttu-id="04920-209">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="04920-209">Click **Add user**.</span></span>

5. <span data-ttu-id="04920-210">Voer het e-mailadres van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="04920-210">Enter the user's email address.</span></span>

6. <span data-ttu-id="04920-211">Kies de rol van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="04920-211">Choose the user's role.</span></span>

7. <span data-ttu-id="04920-212">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="04920-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="04920-213">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="04920-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="04920-214">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Pantheon.</span><span class="sxs-lookup"><span data-stu-id="04920-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="04920-216">**Britta Simon om aan te wijzen Pantheon, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="04920-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="04920-217">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="04920-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="04920-219">Selecteer in de lijst met toepassingen **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="04920-219">In the applications list, select **Pantheon**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="04920-221">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="04920-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="04920-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="04920-223">Click **Add** button.</span></span> <span data-ttu-id="04920-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04920-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="04920-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="04920-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="04920-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04920-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04920-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="04920-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="04920-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="04920-229">Testing single sign-on</span></span>

<span data-ttu-id="04920-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="04920-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="04920-231">Als u op de tegel Pantheon in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Pantheon.</span><span class="sxs-lookup"><span data-stu-id="04920-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="04920-232">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="04920-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="04920-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="04920-233">Additional resources</span></span>

* [<span data-ttu-id="04920-234">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04920-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04920-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="04920-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

