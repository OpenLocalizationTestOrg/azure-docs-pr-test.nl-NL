---
title: 'Zelfstudie: Azure Active Directory-integratie met Learning op het werk | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en het leren op het werk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 941832740689c583a8e857d706c35f3076fa754f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="e45c2-103">Zelfstudie: Azure Active Directory-integratie met Learning op het werk</span><span class="sxs-lookup"><span data-stu-id="e45c2-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="e45c2-104">In deze zelfstudie leert u het leren op het werk integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e45c2-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e45c2-105">Learning op het werk integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e45c2-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e45c2-106">U kunt beheren in Azure AD die toegang tot Learning op het werk heeft</span><span class="sxs-lookup"><span data-stu-id="e45c2-106">You can control in Azure AD who has access to Learning at Work</span></span>
- <span data-ttu-id="e45c2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Learning op het werk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e45c2-107">You can enable your users to automatically get signed-on to Learning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e45c2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e45c2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e45c2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e45c2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e45c2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e45c2-110">Prerequisites</span></span>

<span data-ttu-id="e45c2-111">Voor het configureren van Azure AD-integratie met Learning op het werk, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e45c2-111">To configure Azure AD integration with Learning at Work, you need the following items:</span></span>

- <span data-ttu-id="e45c2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e45c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e45c2-113">Een Learning op werk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e45c2-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e45c2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e45c2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e45c2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e45c2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e45c2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e45c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e45c2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e45c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e45c2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e45c2-118">Scenario description</span></span>
<span data-ttu-id="e45c2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e45c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e45c2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e45c2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e45c2-121">Het toevoegen van Learning op het werk van de galerie</span><span class="sxs-lookup"><span data-stu-id="e45c2-121">Adding Learning at Work from the gallery</span></span>
2. <span data-ttu-id="e45c2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e45c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-the-gallery"></a><span data-ttu-id="e45c2-123">Het toevoegen van Learning op het werk van de galerie</span><span class="sxs-lookup"><span data-stu-id="e45c2-123">Adding Learning at Work from the gallery</span></span>
<span data-ttu-id="e45c2-124">Voor het configureren van de integratie van Learning op het werk met Azure AD, moet u Learning op het werk van de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e45c2-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e45c2-125">**Als u wilt leren toevoegen op het werk uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e45c2-125">**To add Learning at Work from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e45c2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e45c2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e45c2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e45c2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e45c2-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e45c2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e45c2-133">Typ in het zoekvak **Learning op het werk**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-133">In the search box, type **Learning at Work**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="e45c2-135">Selecteer in het deelvenster resultaten **Learning op het werk**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e45c2-135">In the results panel, select **Learning at Work**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e45c2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e45c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e45c2-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Learning op het werk op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e45c2-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e45c2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Learning op het werk is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e45c2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span></span> <span data-ttu-id="e45c2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker weten op het werk tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e45c2-140">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span></span>

<span data-ttu-id="e45c2-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** weten op het werk.</span><span class="sxs-lookup"><span data-stu-id="e45c2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span></span>

<span data-ttu-id="e45c2-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Learning op het werk, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e45c2-142">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e45c2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e45c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e45c2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e45c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e45c2-145">**[Maken van een Learning op werk testgebruiker](#creating-a-learning-at-work-test-user)**  - Learning op het werk dat is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e45c2-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e45c2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e45c2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e45c2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e45c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e45c2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e45c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e45c2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in het leren op werk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e45c2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="e45c2-150">**Voor het configureren van Azure AD eenmalige aanmelding met Learning op het werk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e45c2-150">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="e45c2-151">In de Azure-portal op de **Learning op het werk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-151">In the Azure portal, on the **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e45c2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e45c2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="e45c2-155">Op de **leren op werk domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e45c2-155">On the **Learning at Work Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="e45c2-157">a.</span><span class="sxs-lookup"><span data-stu-id="e45c2-157">a.</span></span> <span data-ttu-id="e45c2-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="e45c2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="e45c2-159">b.</span><span class="sxs-lookup"><span data-stu-id="e45c2-159">b.</span></span> <span data-ttu-id="e45c2-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="e45c2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e45c2-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="e45c2-161">These values are not the real.</span></span> <span data-ttu-id="e45c2-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="e45c2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e45c2-163">Neem contact op met [leren op werk Client ondersteuningsteam](https://www.learninga-z.com/site/contact/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e45c2-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) to get these values.</span></span> 
 
4. <span data-ttu-id="e45c2-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e45c2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="e45c2-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e45c2-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e45c2-168">Op de **leren op werk configuratie** sectie, klikt u op **Learning configureren op het werk** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e45c2-168">On the **Learning at Work Configuration** section, click **Configure Learning at Work** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e45c2-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e45c2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="e45c2-171">Eenmalige aanmelding configureren op **Learning op het werk** zijde, moet u de gedownloade verzenden **Metadata XML**, **SAML entiteit-ID**, **SAML Single Sign-On-Service URL**, en **Sign-Out URL** naar [leren op werk ondersteuning](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="e45c2-171">To configure single sign-on on **Learning at Work** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** to [Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="e45c2-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e45c2-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e45c2-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e45c2-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e45c2-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e45c2-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e45c2-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e45c2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="e45c2-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e45c2-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e45c2-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e45c2-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e45c2-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e45c2-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e45c2-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e45c2-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e45c2-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e45c2-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e45c2-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e45c2-187">a.</span><span class="sxs-lookup"><span data-stu-id="e45c2-187">a.</span></span> <span data-ttu-id="e45c2-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e45c2-189">b.</span><span class="sxs-lookup"><span data-stu-id="e45c2-189">b.</span></span> <span data-ttu-id="e45c2-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e45c2-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e45c2-191">c.</span><span class="sxs-lookup"><span data-stu-id="e45c2-191">c.</span></span> <span data-ttu-id="e45c2-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e45c2-193">d.</span><span class="sxs-lookup"><span data-stu-id="e45c2-193">d.</span></span> <span data-ttu-id="e45c2-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="e45c2-195">Maken van een Learning op werk testgebruiker</span><span class="sxs-lookup"><span data-stu-id="e45c2-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="e45c2-196">In deze sectie maakt maken u een gebruiker met de naam van Britta Simon weten op het werk.</span><span class="sxs-lookup"><span data-stu-id="e45c2-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="e45c2-197">Werken met [leren op werk ondersteuning](https://www.learninga-z.com/site/contact/support) toevoegen van de gebruikers in het leren op werk-platform.</span><span class="sxs-lookup"><span data-stu-id="e45c2-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) to add the users in the Learning at Work platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e45c2-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e45c2-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e45c2-199">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Learning op het werk.</span><span class="sxs-lookup"><span data-stu-id="e45c2-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning at Work.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e45c2-201">**Britta Simon om aan te wijzen Learning op het werk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e45c2-201">**To assign Britta Simon to Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="e45c2-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e45c2-204">Selecteer in de lijst met toepassingen **Learning op het werk**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-204">In the applications list, select **Learning at Work**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="e45c2-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e45c2-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e45c2-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e45c2-208">Click **Add** button.</span></span> <span data-ttu-id="e45c2-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e45c2-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e45c2-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e45c2-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e45c2-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e45c2-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e45c2-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e45c2-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e45c2-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e45c2-214">Testing single sign-on</span></span>

<span data-ttu-id="e45c2-215">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e45c2-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e45c2-216">Als u het leren op werk-tegel in het deelvenster toegang op, u moet ophalen automatisch aangemeld bij uw Learning op werk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e45c2-216">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span></span>
<span data-ttu-id="e45c2-217">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e45c2-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e45c2-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e45c2-218">Additional resources</span></span>

* [<span data-ttu-id="e45c2-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e45c2-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e45c2-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e45c2-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

