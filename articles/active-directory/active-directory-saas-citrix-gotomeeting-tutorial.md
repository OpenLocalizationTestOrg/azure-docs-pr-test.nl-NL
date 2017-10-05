---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix GoToMeeting | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="22a23-103">Zelfstudie: Azure Active Directory-integratie met Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="22a23-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="22a23-104">In deze zelfstudie leert u hoe Citrix GoToMeeting integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22a23-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22a23-105">Citrix GoToMeeting integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="22a23-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="22a23-106">U kunt beheren in Azure AD die toegang tot Citrix GoToMeeting heeft</span><span class="sxs-lookup"><span data-stu-id="22a23-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="22a23-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Citrix GoToMeeting (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="22a23-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22a23-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="22a23-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="22a23-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22a23-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22a23-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="22a23-110">Prerequisites</span></span>

<span data-ttu-id="22a23-111">Voor het configureren van Azure AD-integratie met Citrix GoToMeeting, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="22a23-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="22a23-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="22a23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22a23-113">Een Citrix GoToMeeting eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="22a23-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22a23-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="22a23-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22a23-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="22a23-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22a23-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="22a23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22a23-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22a23-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22a23-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="22a23-118">Scenario description</span></span>
<span data-ttu-id="22a23-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="22a23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22a23-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="22a23-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22a23-121">Citrix GoToMeeting uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="22a23-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="22a23-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="22a23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="22a23-123">Citrix GoToMeeting uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="22a23-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="22a23-124">Voor het configureren van de integratie van Citrix GoToMeeting in Azure AD, moet u Citrix GoToMeeting uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="22a23-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="22a23-125">**Als u wilt toevoegen Citrix GoToMeeting uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22a23-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="22a23-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="22a23-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22a23-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="22a23-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="22a23-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="22a23-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="22a23-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="22a23-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="22a23-133">Typ in het zoekvak **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="22a23-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="22a23-135">Selecteer in het deelvenster resultaten **Citrix GoToMeeting**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="22a23-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22a23-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="22a23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22a23-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Citrix GoToMeeting op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="22a23-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="22a23-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Citrix GoToMeeting is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22a23-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="22a23-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Citrix GoToMeeting tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="22a23-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="22a23-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="22a23-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="22a23-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Citrix GoToMeeting, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="22a23-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="22a23-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22a23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="22a23-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22a23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22a23-145">**[Maken van een testgebruiker Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  - Citrix GoToMeeting die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="22a23-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="22a23-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="22a23-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22a23-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="22a23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22a23-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="22a23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22a23-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Citrix GoToMeeting configureren.</span><span class="sxs-lookup"><span data-stu-id="22a23-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="22a23-150">**Voor het configureren van Azure AD eenmalige aanmelding met Citrix GoToMeeting, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22a23-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="22a23-151">In de Azure-portal op de **Citrix GoToMeeting** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="22a23-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="22a23-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="22a23-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="22a23-155">Op de **Citrix GoToMeeting domein en de URL's** sectie, hoeft u niet alle stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="22a23-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="22a23-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="22a23-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="22a23-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="22a23-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="22a23-161">Klik in de configuratiesectie van Citrix GoToMeeting SAML Citrix GoToMeeting SAML configureren om configureren aanmelding venster te openen.</span><span class="sxs-lookup"><span data-stu-id="22a23-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="22a23-162">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="22a23-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="22a23-163">In een ander browservenster, meld u aan bij uw [Citrix organisatie Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="22a23-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="22a23-164">Klik op de **identiteitsprovider** tabblad en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="22a23-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="22a23-165">![Setup van SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span><span class="sxs-lookup"><span data-stu-id="22a23-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="22a23-166">a.</span><span class="sxs-lookup"><span data-stu-id="22a23-166">a.</span></span> <span data-ttu-id="22a23-167">Selecteer **handmatig**</span><span class="sxs-lookup"><span data-stu-id="22a23-167">Select **Manual**</span></span>

    <span data-ttu-id="22a23-168">b.</span><span class="sxs-lookup"><span data-stu-id="22a23-168">b.</span></span> <span data-ttu-id="22a23-169">In de Azure portal op de **eenmalige aanmelding configureren op Citrix GoToMeeting** dialoogvenster pagina-, Kopieer de **SAML Single Sign-On Service-URL** waarde en plak deze in de **aanmelden pagina-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="22a23-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="22a23-170">c.</span><span class="sxs-lookup"><span data-stu-id="22a23-170">c.</span></span> <span data-ttu-id="22a23-171">In de Azure portal op de **eenmalige aanmelding configureren op Citrix GoToMeeting** dialoogvenster pagina-, Kopieer de **Sign-Out URL** waarde en plak deze in de **afmelden pagina-URL** tekstvak.</span><span class="sxs-lookup"><span data-stu-id="22a23-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="22a23-172">d.</span><span class="sxs-lookup"><span data-stu-id="22a23-172">d.</span></span> <span data-ttu-id="22a23-173">In de Azure portal op de **eenmalige aanmelding configureren op Citrix GoToMeeting** dialoogvenster pagina-, Kopieer de **SAML entiteit-ID** waarde en plak deze in de **identiteit Provider entiteit-ID**textbox.</span><span class="sxs-lookup"><span data-stu-id="22a23-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="22a23-174">e.</span><span class="sxs-lookup"><span data-stu-id="22a23-174">e.</span></span> <span data-ttu-id="22a23-175">Als u wilt uw gedownloade certificaat uploaden, klikt u op **certificaat uploaden**.</span><span class="sxs-lookup"><span data-stu-id="22a23-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="22a23-176">f.</span><span class="sxs-lookup"><span data-stu-id="22a23-176">f.</span></span> <span data-ttu-id="22a23-177">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="22a23-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="22a23-178">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="22a23-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="22a23-179">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="22a23-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="22a23-180">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="22a23-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22a23-181">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="22a23-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="22a23-182">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="22a23-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="22a23-184">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22a23-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="22a23-185">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="22a23-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22a23-187">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="22a23-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22a23-189">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="22a23-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22a23-191">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="22a23-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22a23-193">a.</span><span class="sxs-lookup"><span data-stu-id="22a23-193">a.</span></span> <span data-ttu-id="22a23-194">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22a23-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22a23-195">b.</span><span class="sxs-lookup"><span data-stu-id="22a23-195">b.</span></span> <span data-ttu-id="22a23-196">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="22a23-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22a23-197">c.</span><span class="sxs-lookup"><span data-stu-id="22a23-197">c.</span></span> <span data-ttu-id="22a23-198">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="22a23-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="22a23-199">d.</span><span class="sxs-lookup"><span data-stu-id="22a23-199">d.</span></span> <span data-ttu-id="22a23-200">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="22a23-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="22a23-201">Een testgebruiker Citrix GoToMeeting maken</span><span class="sxs-lookup"><span data-stu-id="22a23-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="22a23-202">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="22a23-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="22a23-203">Citrix GoToMeeting ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="22a23-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="22a23-204">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="22a23-204">There is no action item for you in this section.</span></span> <span data-ttu-id="22a23-205">Als een gebruiker in Citrix GoToMeeting nog niet bestaat, wordt een nieuw gemaakt wanneer u probeert te krijgen tot Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="22a23-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="22a23-206">Als u wilt een gebruiker handmatig maken, neem contact op met [ondersteuningsteam Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="22a23-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="22a23-207">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="22a23-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="22a23-208">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="22a23-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="22a23-210">**Britta Simon om aan te wijzen Citrix GoToMeeting, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="22a23-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="22a23-211">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="22a23-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="22a23-213">Selecteer in de lijst met toepassingen **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="22a23-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="22a23-215">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="22a23-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="22a23-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="22a23-217">Click **Add** button.</span></span> <span data-ttu-id="22a23-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="22a23-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="22a23-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="22a23-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="22a23-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="22a23-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22a23-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="22a23-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="22a23-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="22a23-223">Testing single sign-on</span></span>

<span data-ttu-id="22a23-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="22a23-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="22a23-225">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="22a23-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="22a23-226">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="22a23-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="22a23-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="22a23-227">Additional resources</span></span>

* [<span data-ttu-id="22a23-228">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22a23-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22a23-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="22a23-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="22a23-230">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="22a23-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

