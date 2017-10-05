---
title: 'Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Dropbox voor bedrijven.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="e015a-103">Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="e015a-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="e015a-104">In deze zelfstudie leert u hoe Dropbox voor bedrijven integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e015a-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e015a-105">Dropbox voor bedrijven integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e015a-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e015a-106">U kunt beheren in Azure AD die toegang tot Dropbox voor bedrijven heeft</span><span class="sxs-lookup"><span data-stu-id="e015a-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="e015a-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Dropbox voor bedrijven (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e015a-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e015a-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e015a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e015a-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e015a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e015a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e015a-110">Prerequisites</span></span>

<span data-ttu-id="e015a-111">Voor het configureren van Azure AD-integratie met Dropbox voor bedrijven, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e015a-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="e015a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e015a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e015a-113">Een Dropbox voor eenmalige aanmelding Business abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="e015a-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e015a-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e015a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e015a-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e015a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e015a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e015a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e015a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e015a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e015a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e015a-118">Scenario description</span></span>
<span data-ttu-id="e015a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e015a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e015a-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e015a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e015a-121">Dropbox voor bedrijven uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e015a-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="e015a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e015a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="e015a-123">Dropbox voor bedrijven uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e015a-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="e015a-124">Voor het configureren van de integratie van Dropbox voor bedrijven met Azure AD, moet u Dropbox voor bedrijven uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e015a-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e015a-125">**Als u wilt toevoegen Dropbox voor bedrijven uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e015a-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e015a-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e015a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e015a-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e015a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e015a-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e015a-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e015a-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e015a-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e015a-133">Typ in het zoekvak **Dropbox voor bedrijven**.</span><span class="sxs-lookup"><span data-stu-id="e015a-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="e015a-135">Selecteer in het deelvenster resultaten **Dropbox voor bedrijven**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e015a-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e015a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e015a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e015a-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Dropbox voor bedrijven op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e015a-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e015a-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Dropbox voor bedrijven is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e015a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="e015a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Dropbox voor bedrijven tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e015a-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="e015a-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="e015a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="e015a-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Dropbox voor bedrijven, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e015a-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e015a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e015a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e015a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e015a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e015a-145">**[Maken van een Dropbox voor zakelijke testgebruiker](#creating-a-dropbox-for-business-test-user)**  - Dropbox voor bedrijven die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e015a-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e015a-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e015a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e015a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e015a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e015a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e015a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e015a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw dropbox geplaatst voor Business-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e015a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="e015a-150">**Voor het configureren van Azure AD eenmalige aanmelding met Dropbox voor bedrijven, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e015a-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="e015a-151">In de Azure-portal op de **Dropbox voor bedrijven** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e015a-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e015a-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e015a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="e015a-155">Op de **Dropbox voor Business-domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e015a-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="e015a-156">a.</span><span class="sxs-lookup"><span data-stu-id="e015a-156">a.</span></span> <span data-ttu-id="e015a-157">Meld u aan op uw Dropbox voor bedrijven-tenant.</span><span class="sxs-lookup"><span data-stu-id="e015a-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="e015a-158">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e015a-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="e015a-159">b.</span><span class="sxs-lookup"><span data-stu-id="e015a-159">b.</span></span> <span data-ttu-id="e015a-160">Klik in het navigatievenster aan de linkerkant op **beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="e015a-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="e015a-161">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e015a-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="e015a-162">c.</span><span class="sxs-lookup"><span data-stu-id="e015a-162">c.</span></span> <span data-ttu-id="e015a-163">Op de **beheerconsole**, klikt u op **verificatie** in het navigatiedeelvenster links.</span><span class="sxs-lookup"><span data-stu-id="e015a-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="e015a-164">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e015a-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="e015a-165">d.</span><span class="sxs-lookup"><span data-stu-id="e015a-165">d.</span></span> <span data-ttu-id="e015a-166">In de **eenmalige aanmelding** sectie **eenmalige aanmelding inschakelen**, en klik vervolgens op **meer** uit te breiden in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e015a-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="e015a-167">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e015a-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="e015a-168">e.</span><span class="sxs-lookup"><span data-stu-id="e015a-168">e.</span></span> <span data-ttu-id="e015a-169">Kopieer de URL naast **kunnen gebruikers zich aanmelden door te voeren van het e-mailadres of kunnen ze rechtstreeks naar**.</span><span class="sxs-lookup"><span data-stu-id="e015a-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="e015a-171">f.</span><span class="sxs-lookup"><span data-stu-id="e015a-171">f.</span></span> <span data-ttu-id="e015a-172">Op de Azure-portal in de **aanmeldings-URL** textbox, plak de URL.</span><span class="sxs-lookup"><span data-stu-id="e015a-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="e015a-174">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="e015a-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e015a-175">Deze waarde is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="e015a-175">This value is not real value.</span></span> <span data-ttu-id="e015a-176">Werk de waarde met de werkelijke aanmeldings-URL u via een sectie voor eenmalige aanmelding krijgen.</span><span class="sxs-lookup"><span data-stu-id="e015a-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="e015a-177">Neem contact op met [Dropbox voor Business Client ondersteuningsteam](https://www.dropbox.com/business/contact) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="e015a-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="e015a-178">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e015a-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="e015a-180">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e015a-180">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e015a-182">Op de **Dropbox voor zakelijke configuratie** sectie, klikt u op **Dropbox configureren voor bedrijven** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e015a-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e015a-183">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e015a-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="e015a-185">Eenmalige aanmelding configureren op **Dropbox voor bedrijven** zijde, gaat u in uw Dropbox voor bedrijven-tenant, het **eenmalige aanmelding** sectie van de **verificatie** pagina de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e015a-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="e015a-186">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="e015a-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="e015a-187">a.</span><span class="sxs-lookup"><span data-stu-id="e015a-187">a.</span></span> <span data-ttu-id="e015a-188">Klik op **vereist**.</span><span class="sxs-lookup"><span data-stu-id="e015a-188">Click **Required**.</span></span>
   
    <span data-ttu-id="e015a-189">b.</span><span class="sxs-lookup"><span data-stu-id="e015a-189">b.</span></span> <span data-ttu-id="e015a-190">In de Azure-portal op de **eenmalige aanmelding configureren** venster, Kopieer de **SAML Single Sign-On Service-URL** waarde en plak deze in de **aanmelden URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e015a-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="e015a-191">c.</span><span class="sxs-lookup"><span data-stu-id="e015a-191">c.</span></span> <span data-ttu-id="e015a-192">Klik op **certificaat kiezen**, en blader vervolgens naar uw **Base64-gecodeerde certificaatbestand**.</span><span class="sxs-lookup"><span data-stu-id="e015a-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="e015a-193">d.</span><span class="sxs-lookup"><span data-stu-id="e015a-193">d.</span></span> <span data-ttu-id="e015a-194">Klik op **wijzigingen opslaan** om de configuratie op uw DropBox voor zakelijke tenant te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e015a-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="e015a-195">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e015a-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e015a-196">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e015a-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e015a-197">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e015a-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e015a-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e015a-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="e015a-199">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e015a-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e015a-201">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e015a-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e015a-202">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e015a-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="e015a-204">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e015a-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e015a-206">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e015a-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e015a-208">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e015a-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e015a-210">a.</span><span class="sxs-lookup"><span data-stu-id="e015a-210">a.</span></span> <span data-ttu-id="e015a-211">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e015a-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e015a-212">b.</span><span class="sxs-lookup"><span data-stu-id="e015a-212">b.</span></span> <span data-ttu-id="e015a-213">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e015a-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e015a-214">c.</span><span class="sxs-lookup"><span data-stu-id="e015a-214">c.</span></span> <span data-ttu-id="e015a-215">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e015a-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e015a-216">d.</span><span class="sxs-lookup"><span data-stu-id="e015a-216">d.</span></span> <span data-ttu-id="e015a-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e015a-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="e015a-218">Een Dropbox voor zakelijke testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e015a-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="e015a-219">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="e015a-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="e015a-220">Dropbox voor bedrijven ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e015a-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="e015a-221">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e015a-221">There is no action item for you in this section.</span></span> <span data-ttu-id="e015a-222">Als een gebruiker niet al in Dropbox voor bedrijven bestaat, wordt een nieuw gemaakt wanneer u probeert te krijgen tot Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="e015a-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="e015a-223">Als u wilt een gebruiker handmatig maken, neem contact op met [Dropbox voor Business Client ondersteuningsteam](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="e015a-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e015a-224">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e015a-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e015a-225">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="e015a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e015a-227">**Britta Simon om aan te wijzen Dropbox voor bedrijven, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e015a-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="e015a-228">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e015a-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e015a-230">Selecteer in de lijst met toepassingen **Dropbox voor bedrijven**.</span><span class="sxs-lookup"><span data-stu-id="e015a-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="e015a-232">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e015a-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e015a-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e015a-234">Click **Add** button.</span></span> <span data-ttu-id="e015a-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e015a-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e015a-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e015a-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e015a-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e015a-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e015a-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e015a-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e015a-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e015a-240">Testing single sign-on</span></span>

<span data-ttu-id="e015a-241">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e015a-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e015a-242">Als u klikt op de Dropbox voor bedrijven-tegel in het deelvenster toegang, krijgt u de aanmeldingspagina van uw Dropbox voor Business-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e015a-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e015a-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e015a-243">Additional resources</span></span>

* [<span data-ttu-id="e015a-244">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e015a-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e015a-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e015a-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e015a-246">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="e015a-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

