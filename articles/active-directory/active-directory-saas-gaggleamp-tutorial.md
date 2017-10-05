---
title: 'Zelfstudie: Azure Active Directory-integratie met GaggleAMP | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en GaggleAMP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="cf5d1-103">Zelfstudie: Azure Active Directory-integratie met GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="cf5d1-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="cf5d1-104">In deze zelfstudie leert u hoe GaggleAMP integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf5d1-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf5d1-105">GaggleAMP integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cf5d1-106">U kunt beheren in Azure AD die toegang tot GaggleAMP heeft</span><span class="sxs-lookup"><span data-stu-id="cf5d1-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="cf5d1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij GaggleAMP (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="cf5d1-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf5d1-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="cf5d1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cf5d1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf5d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf5d1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cf5d1-110">Prerequisites</span></span>

<span data-ttu-id="cf5d1-111">Voor het configureren van Azure AD-integratie met GaggleAMP, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="cf5d1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="cf5d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf5d1-113">Een GaggleAMP eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="cf5d1-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf5d1-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf5d1-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf5d1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf5d1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf5d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf5d1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cf5d1-118">Scenario description</span></span>
<span data-ttu-id="cf5d1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf5d1-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf5d1-121">GaggleAMP uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="cf5d1-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="cf5d1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf5d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="cf5d1-123">GaggleAMP uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="cf5d1-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="cf5d1-124">Voor het configureren van de integratie van GaggleAMP in Azure AD, moet u GaggleAMP uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cf5d1-125">**Als u wilt toevoegen GaggleAMP uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf5d1-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cf5d1-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf5d1-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cf5d1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="cf5d1-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="cf5d1-133">Typ in het zoekvak **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-133">In the search box, type **GaggleAMP**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="cf5d1-135">Selecteer in het deelvenster resultaten **GaggleAMP**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf5d1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf5d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf5d1-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met GaggleAMP op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf5d1-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in GaggleAMP is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="cf5d1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in GaggleAMP tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="cf5d1-141">Wijs in GaggleAMP, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cf5d1-142">Om te configureren en testen van Azure AD eenmalige aanmelding met GaggleAMP, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cf5d1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cf5d1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf5d1-145">**[Maken van een testgebruiker GaggleAMP](#creating-a-gaggleamp-test-user)**  - GaggleAMP die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf5d1-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf5d1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf5d1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="cf5d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf5d1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing GaggleAMP configureren.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="cf5d1-150">**Voor het configureren van Azure AD eenmalige aanmelding met GaggleAMP, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf5d1-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="cf5d1-151">In de Azure-portal op de **GaggleAMP** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="cf5d1-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="cf5d1-155">Op de **GaggleAMP domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-155">On the **GaggleAMP Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="cf5d1-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="cf5d1-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cf5d1-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-158">The value is not real.</span></span> <span data-ttu-id="cf5d1-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="cf5d1-160">Neem contact op met [GaggleAMP Client ondersteuningsteam](mailto:sales@gaggleamp.com) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get the value.</span></span> 
 
4. <span data-ttu-id="cf5d1-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="cf5d1-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cf5d1-165">Op de **GaggleAMP configuratie** sectie, klikt u op **configureren GaggleAMP** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-165">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cf5d1-166">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="cf5d1-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="cf5d1-168">In een ander browserexemplaar, Ga naar de SAML SSO-pagina voor u door de Gaggle ondersteuningsteam gemaakt (bijvoorbeeld: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="cf5d1-168">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="cf5d1-169">Op uw **SAML SSO** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-169">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![GaggleAMP voor eenmalige aanmelding](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="cf5d1-171">a.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-171">a.</span></span> <span data-ttu-id="cf5d1-172">In de **identiteit Provider verlener** textbox, plak de waarde van **URL-verlener** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-172">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="cf5d1-173">b.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-173">b.</span></span> <span data-ttu-id="cf5d1-174">In de **identiteit Provider één aanmeldings-URL** textbox, plak de waarde van **Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-174">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="cf5d1-175">c.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-175">c.</span></span> <span data-ttu-id="cf5d1-176">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="cf5d1-176">Click **Save**</span></span>      

    <span data-ttu-id="cf5d1-177">d.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-177">d.</span></span> <span data-ttu-id="cf5d1-178">Verzenden van de **certificaat (Base64)** -certificaat voor uw [GaggleAMP ondersteuningsteam](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="cf5d1-178">Send the **Certificate (Base64)** certificate to your [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="cf5d1-179">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="cf5d1-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cf5d1-180">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cf5d1-181">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf5d1-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf5d1-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cf5d1-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf5d1-183">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="cf5d1-185">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf5d1-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cf5d1-186">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf5d1-188">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf5d1-190">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf5d1-192">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cf5d1-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf5d1-194">a.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-194">a.</span></span> <span data-ttu-id="cf5d1-195">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf5d1-196">b.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-196">b.</span></span> <span data-ttu-id="cf5d1-197">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf5d1-198">c.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-198">c.</span></span> <span data-ttu-id="cf5d1-199">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cf5d1-200">d.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-200">d.</span></span> <span data-ttu-id="cf5d1-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="cf5d1-202">Een testgebruiker GaggleAMP maken</span><span class="sxs-lookup"><span data-stu-id="cf5d1-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="cf5d1-203">Het doel van deze sectie is het maken van een gebruiker Britta Simon in GaggleAMP genoemd.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-203">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="cf5d1-204">GaggleAMP ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cf5d1-205">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-205">There is no action item for you in this section.</span></span> <span data-ttu-id="cf5d1-206">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot GaggleAMP als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-206">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cf5d1-207">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf5d1-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cf5d1-208">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="cf5d1-210">**Britta Simon om aan te wijzen GaggleAMP, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="cf5d1-210">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="cf5d1-211">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="cf5d1-213">Selecteer in de lijst met toepassingen **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-213">In the applications list, select **GaggleAMP**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="cf5d1-215">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="cf5d1-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-217">Click **Add** button.</span></span> <span data-ttu-id="cf5d1-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="cf5d1-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cf5d1-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf5d1-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf5d1-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cf5d1-223">Testing single sign-on</span></span>

<span data-ttu-id="cf5d1-224">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="cf5d1-225">Als u op de tegel GaggleAMP in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="cf5d1-225">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf5d1-226">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cf5d1-226">Additional resources</span></span>

* [<span data-ttu-id="cf5d1-227">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf5d1-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf5d1-228">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf5d1-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

