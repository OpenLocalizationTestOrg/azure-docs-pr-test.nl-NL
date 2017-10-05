---
title: 'Zelfstudie: Azure Active Directory-integratie met StatusPage | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en StatusPage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="3f590-103">Zelfstudie: Azure Active Directory-integratie met StatusPage</span><span class="sxs-lookup"><span data-stu-id="3f590-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="3f590-104">In deze zelfstudie leert u hoe StatusPage integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f590-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f590-105">StatusPage integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3f590-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f590-106">U kunt beheren in Azure AD die toegang tot StatusPage heeft</span><span class="sxs-lookup"><span data-stu-id="3f590-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="3f590-107">U kunt uw gebruikers automatisch ophalen aangemeld bij StatusPage (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3f590-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f590-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3f590-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3f590-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f590-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f590-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f590-110">Prerequisites</span></span>

<span data-ttu-id="3f590-111">Voor het configureren van Azure AD-integratie met StatusPage, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3f590-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="3f590-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3f590-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f590-113">Een StatusPage eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3f590-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f590-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f590-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f590-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3f590-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f590-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3f590-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f590-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f590-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f590-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3f590-118">Scenario description</span></span>
<span data-ttu-id="3f590-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f590-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f590-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3f590-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f590-121">StatusPage uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3f590-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="3f590-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f590-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="3f590-123">StatusPage uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3f590-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="3f590-124">Voor het configureren van de integratie van StatusPage in Azure AD, moet u StatusPage uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3f590-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f590-125">**Als u wilt toevoegen StatusPage uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f590-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f590-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3f590-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f590-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f590-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f590-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f590-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3f590-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f590-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3f590-133">Typ in het zoekvak **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="3f590-133">In the search box, type **StatusPage**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="3f590-135">Selecteer in het deelvenster resultaten **StatusPage**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3f590-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f590-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f590-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f590-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met StatusPage op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3f590-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3f590-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in StatusPage is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f590-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="3f590-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in StatusPage tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3f590-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="3f590-141">Wijs in StatusPage, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="3f590-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3f590-142">Om te configureren en testen van Azure AD eenmalige aanmelding met StatusPage, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3f590-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f590-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f590-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f590-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f590-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f590-145">**[Maken van een testgebruiker StatusPage](#creating-a-statuspage-test-user)**  - StatusPage die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3f590-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f590-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3f590-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f590-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3f590-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f590-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3f590-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f590-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing StatusPage configureren.</span><span class="sxs-lookup"><span data-stu-id="3f590-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="3f590-150">**Voor het configureren van Azure AD eenmalige aanmelding met StatusPage, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f590-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="3f590-151">In de Azure-portal op de **StatusPage** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3f590-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3f590-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3f590-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="3f590-155">Op de **StatusPage domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3f590-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="3f590-157">a.</span><span class="sxs-lookup"><span data-stu-id="3f590-157">a.</span></span> <span data-ttu-id="3f590-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="3f590-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="3f590-159">b.</span><span class="sxs-lookup"><span data-stu-id="3f590-159">b.</span></span> <span data-ttu-id="3f590-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="3f590-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="3f590-161">Neem contact op met het ondersteuningsteam StatusPage op [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)om aan te vragen van de metagegevens die nodig zijn voor het configureren van eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3f590-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="3f590-162">a.</span><span class="sxs-lookup"><span data-stu-id="3f590-162">a.</span></span> <span data-ttu-id="3f590-163">Kopieer de waarde van de verlener van de metagegevens en plakt u deze in de **id** textbox.</span><span class="sxs-lookup"><span data-stu-id="3f590-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="3f590-164">b.</span><span class="sxs-lookup"><span data-stu-id="3f590-164">b.</span></span> <span data-ttu-id="3f590-165">Kopieer de URL van het antwoord van de metagegevens en plakt u deze in de **antwoord-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3f590-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="3f590-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3f590-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="3f590-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3f590-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3f590-170">Op de **StatusPage configuratie** sectie, klikt u op **configureren StatusPage** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3f590-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3f590-171">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3f590-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="3f590-173">In een ander browservenster zich aanmelden bij uw bedrijf StatusPage site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="3f590-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="3f590-174">Klik in de hoofdwerkbalk **Account beheren**.</span><span class="sxs-lookup"><span data-stu-id="3f590-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="3f590-176">Klik op de **Single Sign-on** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3f590-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="3f590-178">Voer de volgende stappen uit op de installatiepagina van eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="3f590-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="3f590-181">a.</span><span class="sxs-lookup"><span data-stu-id="3f590-181">a.</span></span> <span data-ttu-id="3f590-182">In de **doel-URL voor eenmalige aanmelding** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3f590-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3f590-183">b.</span><span class="sxs-lookup"><span data-stu-id="3f590-183">b.</span></span> <span data-ttu-id="3f590-184">Open uw gedownloade certificaat in Kladblok, Kopieer de inhoud en plakt u deze in de **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="3f590-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="3f590-185">c.</span><span class="sxs-lookup"><span data-stu-id="3f590-185">c.</span></span> <span data-ttu-id="3f590-186">Klik op **configuratie opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3f590-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="3f590-187">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3f590-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3f590-188">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3f590-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3f590-189">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f590-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f590-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3f590-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f590-191">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3f590-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3f590-193">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f590-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f590-194">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3f590-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f590-196">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3f590-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f590-198">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f590-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f590-200">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3f590-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f590-202">a.</span><span class="sxs-lookup"><span data-stu-id="3f590-202">a.</span></span> <span data-ttu-id="3f590-203">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f590-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f590-204">b.</span><span class="sxs-lookup"><span data-stu-id="3f590-204">b.</span></span> <span data-ttu-id="3f590-205">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3f590-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f590-206">c.</span><span class="sxs-lookup"><span data-stu-id="3f590-206">c.</span></span> <span data-ttu-id="3f590-207">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3f590-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3f590-208">d.</span><span class="sxs-lookup"><span data-stu-id="3f590-208">d.</span></span> <span data-ttu-id="3f590-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f590-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="3f590-210">Een testgebruiker StatusPage maken</span><span class="sxs-lookup"><span data-stu-id="3f590-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="3f590-211">Het doel van deze sectie is het maken van een gebruiker Britta Simon in StatusPage genoemd.</span><span class="sxs-lookup"><span data-stu-id="3f590-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="3f590-212">StatusPage ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="3f590-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="3f590-213">U hebt al ingeschakeld in [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="3f590-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="3f590-214">**Als u wilt een gebruiker Britta Simon aangeroepen in StatusPage maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f590-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="3f590-215">Aanmelding bij uw bedrijf StatusPage site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3f590-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="3f590-216">Klik in het menu bovenaan op **Account beheren**.</span><span class="sxs-lookup"><span data-stu-id="3f590-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="3f590-218">Klik op de **teamleden** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3f590-218">Click the **Team Members** tab.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="3f590-220">Klik op **toevoegen TEAMLID**.</span><span class="sxs-lookup"><span data-stu-id="3f590-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="3f590-222">Typ de **e-mailadres**, **voornaam**, en **achternaam** van een geldige gebruiker die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="3f590-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="3f590-224">Als **rol**, kies **Client Administrator**.</span><span class="sxs-lookup"><span data-stu-id="3f590-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="3f590-225">Klik op **ACCOUNT maken**.</span><span class="sxs-lookup"><span data-stu-id="3f590-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3f590-226">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f590-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3f590-227">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan StatusPage.</span><span class="sxs-lookup"><span data-stu-id="3f590-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3f590-229">**Britta Simon om aan te wijzen StatusPage, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3f590-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="3f590-230">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f590-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3f590-232">Selecteer in de lijst met toepassingen **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="3f590-232">In the applications list, select **StatusPage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="3f590-234">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3f590-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3f590-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3f590-236">Click **Add** button.</span></span> <span data-ttu-id="3f590-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f590-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3f590-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3f590-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f590-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f590-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f590-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f590-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f590-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f590-242">Testing single sign-on</span></span>

<span data-ttu-id="3f590-243">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="3f590-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3f590-244">Als u op de tegel StatusPage in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing StatusPage.</span><span class="sxs-lookup"><span data-stu-id="3f590-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f590-245">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3f590-245">Additional resources</span></span>

* [<span data-ttu-id="3f590-246">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f590-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f590-247">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f590-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

