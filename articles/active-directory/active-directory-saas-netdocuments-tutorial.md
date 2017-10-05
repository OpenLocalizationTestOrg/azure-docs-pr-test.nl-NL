---
title: 'Zelfstudie: Azure Active Directory-integratie met NetDocuments | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en NetDocuments.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="c0401-103">Zelfstudie: Azure Active Directory-integratie met NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c0401-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="c0401-104">In deze zelfstudie leert u hoe NetDocuments integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0401-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0401-105">NetDocuments integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c0401-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0401-106">U kunt beheren in Azure AD die toegang tot NetDocuments heeft</span><span class="sxs-lookup"><span data-stu-id="c0401-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="c0401-107">U kunt uw gebruikers automatisch ophalen aangemeld bij NetDocuments (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c0401-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0401-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c0401-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0401-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0401-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0401-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c0401-110">Prerequisites</span></span>

<span data-ttu-id="c0401-111">Voor het configureren van Azure AD-integratie met NetDocuments, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c0401-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="c0401-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c0401-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0401-113">Een NetDocuments eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c0401-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0401-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c0401-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0401-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c0401-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0401-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c0401-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0401-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0401-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0401-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c0401-118">Scenario description</span></span>
<span data-ttu-id="c0401-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c0401-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0401-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c0401-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0401-121">NetDocuments uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c0401-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="c0401-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c0401-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="c0401-123">NetDocuments uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c0401-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="c0401-124">Voor het configureren van de integratie van NetDocuments in Azure AD, moet u NetDocuments uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c0401-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0401-125">**Als u wilt toevoegen NetDocuments uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0401-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0401-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c0401-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0401-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c0401-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0401-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c0401-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c0401-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0401-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c0401-133">Typ in het zoekvak **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="c0401-133">In the search box, type **NetDocuments**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="c0401-135">Selecteer in het deelvenster resultaten **NetDocuments**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c0401-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0401-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c0401-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0401-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met NetDocuments op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c0401-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0401-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in NetDocuments is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0401-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="c0401-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in NetDocuments tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c0401-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="c0401-141">Wijs in NetDocuments, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c0401-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0401-142">Om te configureren en testen van Azure AD eenmalige aanmelding met NetDocuments, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c0401-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0401-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c0401-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0401-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0401-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0401-145">**[Maken van een testgebruiker NetDocuments](#creating-a-netdocuments-test-user)**  - NetDocuments die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c0401-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0401-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c0401-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0401-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c0401-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0401-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c0401-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0401-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing NetDocuments configureren.</span><span class="sxs-lookup"><span data-stu-id="c0401-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="c0401-150">**Voor het configureren van Azure AD eenmalige aanmelding met NetDocuments, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0401-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="c0401-151">In de Azure-portal op de **NetDocuments** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c0401-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c0401-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c0401-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="c0401-155">Op de **NetDocuments domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c0401-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="c0401-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0401-157">a.</span></span> <span data-ttu-id="c0401-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="c0401-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="c0401-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0401-159">b.</span></span> <span data-ttu-id="c0401-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="c0401-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0401-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c0401-161">These values are not real.</span></span> <span data-ttu-id="c0401-162">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="c0401-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="c0401-163">Neem contact op met [NetDocuments ondersteuningsteam](https://support.netdocuments.com/hc/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c0401-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="c0401-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c0401-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="c0401-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c0401-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0401-168">In een ander browservenster, meld u bij uw bedrijf NetDocuments site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c0401-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="c0401-169">Ga naar **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c0401-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="c0401-170">Klik op **toevoegen en verwijderen van gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c0401-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="c0401-171">![Opslagplaats](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "opslagplaats")</span><span class="sxs-lookup"><span data-stu-id="c0401-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="c0401-172">Klik op **geavanceerde verificatieopties configureren**.</span><span class="sxs-lookup"><span data-stu-id="c0401-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="c0401-173">![Configureer geavanceerde verificatieopties](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "geavanceerde verificatieopties configureren")</span><span class="sxs-lookup"><span data-stu-id="c0401-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="c0401-174">Op de **federatieve identiteit** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c0401-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c0401-175">![Federatieve Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "federatieve Identitty")</span><span class="sxs-lookup"><span data-stu-id="c0401-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="c0401-176">a.</span><span class="sxs-lookup"><span data-stu-id="c0401-176">a.</span></span> <span data-ttu-id="c0401-177">Als **federatieve identiteit servertype**, selecteer **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="c0401-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="c0401-178">b.</span><span class="sxs-lookup"><span data-stu-id="c0401-178">b.</span></span> <span data-ttu-id="c0401-179">Klik op **bestand kiezen**, voor het uploaden van het gedownloade metagegevensbestand dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c0401-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="c0401-180">c.</span><span class="sxs-lookup"><span data-stu-id="c0401-180">c.</span></span> <span data-ttu-id="c0401-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0401-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="c0401-182">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c0401-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0401-183">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c0401-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0401-184">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0401-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0401-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c0401-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0401-186">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c0401-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c0401-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0401-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0401-189">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c0401-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0401-191">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c0401-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0401-193">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0401-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0401-195">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c0401-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0401-197">a.</span><span class="sxs-lookup"><span data-stu-id="c0401-197">a.</span></span> <span data-ttu-id="c0401-198">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0401-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0401-199">b.</span><span class="sxs-lookup"><span data-stu-id="c0401-199">b.</span></span> <span data-ttu-id="c0401-200">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0401-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0401-201">c.</span><span class="sxs-lookup"><span data-stu-id="c0401-201">c.</span></span> <span data-ttu-id="c0401-202">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c0401-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0401-203">d.</span><span class="sxs-lookup"><span data-stu-id="c0401-203">d.</span></span> <span data-ttu-id="c0401-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c0401-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="c0401-205">Een testgebruiker NetDocuments maken</span><span class="sxs-lookup"><span data-stu-id="c0401-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="c0401-206">Om Azure AD-gebruikers zich aanmelden bij NetDocuments, moeten ze worden ingericht in NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c0401-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="c0401-207">In het geval van NetDocuments is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c0401-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="c0401-208">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0401-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c0401-209">Sing aan bij uw **NetDocuments** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="c0401-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="c0401-210">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c0401-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="c0401-211">![Beheerder](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c0401-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="c0401-212">Klik op **toevoegen en verwijderen van gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c0401-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="c0401-213">![Opslagplaats](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "opslagplaats")</span><span class="sxs-lookup"><span data-stu-id="c0401-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="c0401-214">In de **e-mailadres** textbox, typ de e-mailadres van een geldige Azure Active Directory-account dat u wilt inrichten, en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c0401-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="c0401-215">![E-mailadres](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "e-mailadres")</span><span class="sxs-lookup"><span data-stu-id="c0401-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c0401-216">De houder van Azure Active Directory-account ontvangt een e-mailbericht een koppeling om te bevestigen van het account bevat voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="c0401-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="c0401-217">U kunt andere NetDocuments gebruiker account hulpmiddelen voor het maken of API's geleverd door NetDocuments om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c0401-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0401-218">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0401-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0401-219">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c0401-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c0401-221">**Britta Simon om aan te wijzen NetDocuments, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c0401-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="c0401-222">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c0401-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c0401-224">Selecteer in de lijst met toepassingen **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="c0401-224">In the applications list, select **NetDocuments**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="c0401-226">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c0401-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c0401-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c0401-228">Click **Add** button.</span></span> <span data-ttu-id="c0401-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0401-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c0401-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c0401-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0401-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0401-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0401-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c0401-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0401-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c0401-234">Testing single sign-on</span></span>

<span data-ttu-id="c0401-235">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c0401-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0401-236">Als u op de tegel NetDocuments in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c0401-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="c0401-237">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0401-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0401-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c0401-238">Additional resources</span></span>

* [<span data-ttu-id="c0401-239">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0401-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0401-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0401-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

