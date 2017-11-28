---
title: 'Zelfstudie: Azure Active Directory-integratie met Wingspan eTMF | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Wingspan eTMF.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 8c76fb64229abcad0cabb910e7c170979a79d839
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="d3d69-103">Zelfstudie: Azure Active Directory-integratie met Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="d3d69-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="d3d69-104">In deze zelfstudie leert u hoe Wingspan eTMF integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3d69-104">In this tutorial, you learn how to integrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3d69-105">Wingspan eTMF integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d3d69-105">Integrating Wingspan eTMF with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3d69-106">U kunt beheren in Azure AD die toegang tot Wingspan eTMF heeft</span><span class="sxs-lookup"><span data-stu-id="d3d69-106">You can control in Azure AD who has access to Wingspan eTMF</span></span>
- <span data-ttu-id="d3d69-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Wingspan eTMF (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d3d69-107">You can enable your users to automatically get signed-on to Wingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3d69-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d3d69-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3d69-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3d69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3d69-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d3d69-110">Prerequisites</span></span>

<span data-ttu-id="d3d69-111">Voor het configureren van Azure AD-integratie met Wingspan eTMF, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d3d69-111">To configure Azure AD integration with Wingspan eTMF, you need the following items:</span></span>

- <span data-ttu-id="d3d69-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d3d69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3d69-113">Een Wingspan eTMF eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d3d69-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3d69-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d3d69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3d69-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d3d69-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3d69-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d3d69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3d69-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3d69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3d69-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d3d69-118">Scenario description</span></span>
<span data-ttu-id="d3d69-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d3d69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3d69-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d3d69-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3d69-121">Wingspan eTMF uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d3d69-121">Adding Wingspan eTMF from the gallery</span></span>
2. <span data-ttu-id="d3d69-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d3d69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-the-gallery"></a><span data-ttu-id="d3d69-123">Wingspan eTMF uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d3d69-123">Adding Wingspan eTMF from the gallery</span></span>
<span data-ttu-id="d3d69-124">Voor het configureren van de integratie van Wingspan eTMF in Azure AD, moet u Wingspan eTMF uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d3d69-124">To configure the integration of Wingspan eTMF into Azure AD, you need to add Wingspan eTMF from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3d69-125">**Als u wilt toevoegen Wingspan eTMF uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d3d69-125">**To add Wingspan eTMF from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3d69-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d3d69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3d69-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3d69-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d3d69-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3d69-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d3d69-133">Typ in het zoekvak **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-133">In the search box, type **Wingspan eTMF**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="d3d69-135">Selecteer in het deelvenster resultaten **Wingspan eTMF**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3d69-135">In the results panel, select **Wingspan eTMF**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3d69-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d3d69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3d69-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Wingspan eTMF op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d3d69-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d3d69-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Wingspan eTMF is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3d69-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wingspan eTMF is to a user in Azure AD.</span></span> <span data-ttu-id="d3d69-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Wingspan eTMF tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d3d69-140">In other words, a link relationship between an Azure AD user and the related user in Wingspan eTMF needs to be established.</span></span>

<span data-ttu-id="d3d69-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="d3d69-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="d3d69-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Wingspan eTMF, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d3d69-142">To configure and test Azure AD single sign-on with Wingspan eTMF, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3d69-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3d69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3d69-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3d69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3d69-145">**[Maken van een gebruiker Wingspan eTMF test](#creating-a-wingspan-etmf-test-user)**  - hebben een equivalent van Britta Simon in Wingspan eTMF die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d3d69-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - to have a counterpart of Britta Simon in Wingspan eTMF that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3d69-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d3d69-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3d69-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d3d69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3d69-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d3d69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3d69-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Wingspan eTMF-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3d69-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="d3d69-150">**Voor het configureren van Azure AD eenmalige aanmelding met Wingspan eTMF, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d3d69-150">**To configure Azure AD single sign-on with Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="d3d69-151">In de Azure-portal op de **Wingspan eTMF** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-151">In the Azure portal, on the **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d3d69-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d3d69-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="d3d69-155">Op de **Wingspan eTMF domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d3d69-155">On the **Wingspan eTMF Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="d3d69-157">a.</span><span class="sxs-lookup"><span data-stu-id="d3d69-157">a.</span></span> <span data-ttu-id="d3d69-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="d3d69-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="d3d69-159">b.</span><span class="sxs-lookup"><span data-stu-id="d3d69-159">b.</span></span> <span data-ttu-id="d3d69-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="d3d69-160">In the **Identifier** textbox, type a URL using the following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="d3d69-161">c.</span><span class="sxs-lookup"><span data-stu-id="d3d69-161">c.</span></span> <span data-ttu-id="d3d69-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="d3d69-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d3d69-163">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="d3d69-163">These values are not the real.</span></span> <span data-ttu-id="d3d69-164">Deze waarden bijwerken met de werkelijke aanmeldings-URL, -id en antwoord-URL in met de werkelijke klanten en exemplaarnaam.</span><span class="sxs-lookup"><span data-stu-id="d3d69-164">Update these values with the actual Sign-On URL, Identifier and Reply URL including the actual customer name and instance name.</span></span> <span data-ttu-id="d3d69-165">Neem contact op met [Wingspan eTMF Client ondersteuningsteam](http://www.wingspan.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d3d69-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="d3d69-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d3d69-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="d3d69-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d3d69-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d3d69-170">Eenmalige aanmelding configureren op **Wingspan eTMF** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Wingspan eTMF ondersteuning](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="d3d69-170">To configure single sign-on on **Wingspan eTMF** side, you need to send the downloaded **Metadata XML** to [Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="d3d69-171">Ze instellen dit de SAML SSO-verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="d3d69-171">They set this up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3d69-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d3d69-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3d69-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d3d69-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3d69-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3d69-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3d69-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d3d69-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3d69-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d3d69-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d3d69-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d3d69-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3d69-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d3d69-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3d69-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3d69-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3d69-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3d69-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d3d69-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3d69-187">a.</span><span class="sxs-lookup"><span data-stu-id="d3d69-187">a.</span></span> <span data-ttu-id="d3d69-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3d69-189">b.</span><span class="sxs-lookup"><span data-stu-id="d3d69-189">b.</span></span> <span data-ttu-id="d3d69-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3d69-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3d69-191">c.</span><span class="sxs-lookup"><span data-stu-id="d3d69-191">c.</span></span> <span data-ttu-id="d3d69-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3d69-193">d.</span><span class="sxs-lookup"><span data-stu-id="d3d69-193">d.</span></span> <span data-ttu-id="d3d69-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="d3d69-195">Maken van een gebruiker Wingspan eTMF testen</span><span class="sxs-lookup"><span data-stu-id="d3d69-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="d3d69-196">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Wingspan eTMF maken.</span><span class="sxs-lookup"><span data-stu-id="d3d69-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="d3d69-197">Werken met [Wingspan eTMF ondersteuning](http://www.wingspan.com/contact-us/) de gebruikers in de Wingspan eTMF-toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d3d69-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) to add the users in the Wingspan eTMF application.</span></span> <span data-ttu-id="d3d69-198">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3d69-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3d69-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3d69-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3d69-200">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="d3d69-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wingspan eTMF.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d3d69-202">**Britta Simon om aan te wijzen Wingspan eTMF, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d3d69-202">**To assign Britta Simon to Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="d3d69-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d3d69-205">Selecteer in de lijst met toepassingen **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-205">In the applications list, select **Wingspan eTMF**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="d3d69-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d3d69-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d3d69-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d3d69-209">Click **Add** button.</span></span> <span data-ttu-id="d3d69-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3d69-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d3d69-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d3d69-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3d69-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3d69-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3d69-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d3d69-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3d69-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d3d69-215">Testing single sign-on</span></span>

<span data-ttu-id="d3d69-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d3d69-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="d3d69-217">Klik op de tegel Wingspan eTMF in het deelvenster toegang, wordt u omgeleid naar de organisatie aanmelding op de pagina.</span><span class="sxs-lookup"><span data-stu-id="d3d69-217">Click the Wingspan eTMF tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="d3d69-218">Na een geslaagde aanmelding u zal worden aangemeld bij uw Wingspan eTMF-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3d69-218">After successful login, you will be signed-on to your Wingspan eTMF application.</span></span> <span data-ttu-id="d3d69-219">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d3d69-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3d69-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d3d69-220">Additional resources</span></span>

* [<span data-ttu-id="d3d69-221">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3d69-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3d69-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3d69-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

