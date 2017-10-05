---
title: 'Zelfstudie: Azure Active Directory-integratie met UltiPro | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en UltiPro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: ab60bda1be7101d5bd0c51f5499a820db40375bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="57b67-103">Zelfstudie: Azure Active Directory-integratie met UltiPro</span><span class="sxs-lookup"><span data-stu-id="57b67-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="57b67-104">In deze zelfstudie leert u hoe UltiPro integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57b67-104">In this tutorial, you learn how to integrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57b67-105">UltiPro integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="57b67-105">Integrating UltiPro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57b67-106">U kunt beheren in Azure AD die toegang tot UltiPro heeft</span><span class="sxs-lookup"><span data-stu-id="57b67-106">You can control in Azure AD who has access to UltiPro</span></span>
- <span data-ttu-id="57b67-107">U kunt uw gebruikers automatisch ophalen aangemeld bij UltiPro (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="57b67-107">You can enable your users to automatically get signed-on to UltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57b67-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="57b67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57b67-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57b67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57b67-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="57b67-110">Prerequisites</span></span>

<span data-ttu-id="57b67-111">Voor het configureren van Azure AD-integratie met UltiPro, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="57b67-111">To configure Azure AD integration with UltiPro, you need the following items:</span></span>

- <span data-ttu-id="57b67-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="57b67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57b67-113">Een UltiPro eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="57b67-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57b67-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="57b67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57b67-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="57b67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57b67-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="57b67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57b67-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57b67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57b67-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="57b67-118">Scenario description</span></span>
<span data-ttu-id="57b67-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="57b67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57b67-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="57b67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57b67-121">UltiPro uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="57b67-121">Adding UltiPro from the gallery</span></span>
2. <span data-ttu-id="57b67-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57b67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-the-gallery"></a><span data-ttu-id="57b67-123">UltiPro uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="57b67-123">Adding UltiPro from the gallery</span></span>
<span data-ttu-id="57b67-124">Voor het configureren van de integratie van UltiPro in Azure AD, moet u UltiPro uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="57b67-124">To configure the integration of UltiPro into Azure AD, you need to add UltiPro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57b67-125">**Als u wilt toevoegen UltiPro uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57b67-125">**To add UltiPro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57b67-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57b67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57b67-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57b67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57b67-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57b67-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="57b67-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57b67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="57b67-133">Typ in het zoekvak **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="57b67-133">In the search box, type **UltiPro**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="57b67-135">Selecteer in het deelvenster resultaten **UltiPro**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="57b67-135">In the results panel, select **UltiPro**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57b67-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57b67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57b67-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met UltiPro op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="57b67-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57b67-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in UltiPro is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57b67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UltiPro is to a user in Azure AD.</span></span> <span data-ttu-id="57b67-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in UltiPro tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="57b67-140">In other words, a link relationship between an Azure AD user and the related user in UltiPro needs to be established.</span></span>

<span data-ttu-id="57b67-141">Wijs in UltiPro, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="57b67-141">In UltiPro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="57b67-142">Om te configureren en testen van Azure AD eenmalige aanmelding met UltiPro, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="57b67-142">To configure and test Azure AD single sign-on with UltiPro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57b67-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="57b67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57b67-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57b67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57b67-145">**[Maken van een testgebruiker UltiPro](#creating-a-ultipro-test-user)**  - UltiPro die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="57b67-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - to have a counterpart of Britta Simon in UltiPro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57b67-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="57b67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57b67-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="57b67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57b67-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="57b67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57b67-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing UltiPro configureren.</span><span class="sxs-lookup"><span data-stu-id="57b67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="57b67-150">**Voor het configureren van Azure AD eenmalige aanmelding met UltiPro, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57b67-150">**To configure Azure AD single sign-on with UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="57b67-151">In de Azure-portal op de **UltiPro** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="57b67-151">In the Azure portal, on the **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="57b67-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="57b67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="57b67-155">Op de **UltiPro domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="57b67-155">On the **UltiPro Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="57b67-157">a.</span><span class="sxs-lookup"><span data-stu-id="57b67-157">a.</span></span> <span data-ttu-id="57b67-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="57b67-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="57b67-159">b.</span><span class="sxs-lookup"><span data-stu-id="57b67-159">b.</span></span> <span data-ttu-id="57b67-160">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="57b67-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="57b67-161">c.</span><span class="sxs-lookup"><span data-stu-id="57b67-161">c.</span></span> <span data-ttu-id="57b67-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="57b67-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="57b67-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="57b67-163">These values are not real.</span></span> <span data-ttu-id="57b67-164">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="57b67-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="57b67-165">Neem contact op met [UltiPro Client ondersteuningsteam](https://www.ultimatesoftware.com/ContactUs) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="57b67-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) to get these values.</span></span> 

5. <span data-ttu-id="57b67-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="57b67-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="57b67-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="57b67-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="57b67-170">Op de **UltiPro configuratie** sectie, klikt u op **configureren UltiPro** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="57b67-170">On the **UltiPro Configuration** section, click **Configure UltiPro** to open **Configure sign-on** window.</span></span> <span data-ttu-id="57b67-171">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="57b67-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="57b67-173">Eenmalige aanmelding configureren op **UltiPro** zijde, moet u de gedownloade verzenden **Certificate(Base64), Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [UltiPro-ondersteuning team](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="57b67-173">To configure single sign-on on **UltiPro** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="57b67-174">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="57b67-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57b67-175">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="57b67-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57b67-176">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57b67-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57b67-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="57b67-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="57b67-178">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="57b67-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="57b67-180">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57b67-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57b67-181">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57b67-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57b67-183">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="57b67-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57b67-185">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57b67-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57b67-187">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="57b67-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57b67-189">a.</span><span class="sxs-lookup"><span data-stu-id="57b67-189">a.</span></span> <span data-ttu-id="57b67-190">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57b67-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57b67-191">b.</span><span class="sxs-lookup"><span data-stu-id="57b67-191">b.</span></span> <span data-ttu-id="57b67-192">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57b67-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57b67-193">c.</span><span class="sxs-lookup"><span data-stu-id="57b67-193">c.</span></span> <span data-ttu-id="57b67-194">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="57b67-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57b67-195">d.</span><span class="sxs-lookup"><span data-stu-id="57b67-195">d.</span></span> <span data-ttu-id="57b67-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="57b67-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="57b67-197">Een testgebruiker UltiPro maken</span><span class="sxs-lookup"><span data-stu-id="57b67-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="57b67-198">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in UltiPro maken.</span><span class="sxs-lookup"><span data-stu-id="57b67-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="57b67-199">Werken met [UltiPro ondersteuningsteam](https://www.ultimatesoftware.com/ContactUs) de gebruikers van het platform UltiPro toevoegen.</span><span class="sxs-lookup"><span data-stu-id="57b67-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add the users in the UltiPro platform.</span></span> <span data-ttu-id="57b67-200">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="57b67-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57b67-201">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="57b67-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57b67-202">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan UltiPro.</span><span class="sxs-lookup"><span data-stu-id="57b67-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UltiPro.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="57b67-204">**Britta Simon om aan te wijzen UltiPro, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57b67-204">**To assign Britta Simon to UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="57b67-205">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57b67-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="57b67-207">Selecteer in de lijst met toepassingen **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="57b67-207">In the applications list, select **UltiPro**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="57b67-209">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="57b67-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="57b67-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="57b67-211">Click **Add** button.</span></span> <span data-ttu-id="57b67-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57b67-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="57b67-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="57b67-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57b67-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57b67-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57b67-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57b67-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57b67-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57b67-217">Testing single sign-on</span></span>

<span data-ttu-id="57b67-218">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="57b67-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="57b67-219">Als u op de tegel UltiPro in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing UltiPro.</span><span class="sxs-lookup"><span data-stu-id="57b67-219">When you click the UltiPro tile in the Access Panel, you should get automatically signed-on to your UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57b67-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="57b67-220">Additional resources</span></span>

* [<span data-ttu-id="57b67-221">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57b67-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57b67-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57b67-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png

