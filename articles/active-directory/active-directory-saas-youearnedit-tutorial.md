---
title: 'Zelfstudie: Azure Active Directory-integratie met YouEarnedIt | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en YouEarnedIt.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="4d1e2-103">Zelfstudie: Azure Active Directory-integratie met YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="4d1e2-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="4d1e2-104">In deze zelfstudie leert u hoe YouEarnedIt integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d1e2-105">YouEarnedIt integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4d1e2-106">U kunt beheren in Azure AD die toegang tot YouEarnedIt heeft.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="4d1e2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij YouEarnedIt (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4d1e2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4d1e2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d1e2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4d1e2-110">Prerequisites</span></span>

<span data-ttu-id="4d1e2-111">Voor het configureren van Azure AD-integratie met YouEarnedIt, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="4d1e2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4d1e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d1e2-113">Een YouEarnedIt eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4d1e2-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d1e2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d1e2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d1e2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d1e2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d1e2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4d1e2-118">Scenario description</span></span>
<span data-ttu-id="4d1e2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d1e2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d1e2-121">YouEarnedIt uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4d1e2-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="4d1e2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4d1e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="4d1e2-123">YouEarnedIt uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4d1e2-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="4d1e2-124">Voor het configureren van de integratie van YouEarnedIt in Azure AD, moet u YouEarnedIt uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d1e2-125">**Als u wilt toevoegen YouEarnedIt uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1e2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="4d1e2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4d1e2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="4d1e2-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="4d1e2-133">Typ in het zoekvak **YouEarnedt**, selecteer **YouEarnedt** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![YouEarnedIt in de lijst met resultaten](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4d1e2-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1e2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4d1e2-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met YouEarnedIt op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d1e2-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in YouEarnedIt is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="4d1e2-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in YouEarnedIt tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="4d1e2-139">Wijs in YouEarnedIt, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4d1e2-140">Om te configureren en testen van Azure AD eenmalige aanmelding met YouEarnedIt, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d1e2-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d1e2-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d1e2-143">**[Maak een testgebruiker YouEarnedIt](#create-a-youearnedit-test-user)**  - YouEarnedIt die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d1e2-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d1e2-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4d1e2-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4d1e2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4d1e2-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing YouEarnedIt configureren.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="4d1e2-148">**Voor het configureren van Azure AD eenmalige aanmelding met YouEarnedIt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1e2-149">In de Azure-portal op de **YouEarnedIt** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4d1e2-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="4d1e2-153">Op de **YouEarnedIt domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en YouEarnedIt domein eenmalige aanmelding informatie](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="4d1e2-155">a.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-155">a.</span></span> <span data-ttu-id="4d1e2-156">In de **aanmeldings-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="4d1e2-157">Omgeving</span><span class="sxs-lookup"><span data-stu-id="4d1e2-157">Environment</span></span>  | <span data-ttu-id="4d1e2-158">patroon</span><span class="sxs-lookup"><span data-stu-id="4d1e2-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="4d1e2-159">Productie</span><span class="sxs-lookup"><span data-stu-id="4d1e2-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="4d1e2-160">Sandbox</span><span class="sxs-lookup"><span data-stu-id="4d1e2-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="4d1e2-161">b.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-161">b.</span></span> <span data-ttu-id="4d1e2-162">In de **id** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="4d1e2-163">Omgeving</span><span class="sxs-lookup"><span data-stu-id="4d1e2-163">Environment</span></span>  | <span data-ttu-id="4d1e2-164">patroon</span><span class="sxs-lookup"><span data-stu-id="4d1e2-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="4d1e2-165">Productie</span><span class="sxs-lookup"><span data-stu-id="4d1e2-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="4d1e2-166">Sandbox</span><span class="sxs-lookup"><span data-stu-id="4d1e2-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="4d1e2-167">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-167">These values are not real.</span></span> <span data-ttu-id="4d1e2-168">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4d1e2-169">Neem contact op met [YouEarnedIt Client ondersteuningsteam](https://youearnedit.freshdesk.com/support/tickets/new) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="4d1e2-170">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="4d1e2-172">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-172">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d1e2-174">Op de **YouEarnedIt configuratie** sectie, klikt u op **configureren YouEarnedIt** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4d1e2-175">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![YouEarnedIt configuratie](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="4d1e2-177">Eenmalige aanmelding configureren op **YouEarnedIt** zijde, moet u de gedownloade verzenden **Certificate(Base64)** en **SAML Single Sign-On Service-URL** naar [YouEarnedIt ondersteuningsteam](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="4d1e2-178">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4d1e2-179">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="4d1e2-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4d1e2-180">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4d1e2-181">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d1e2-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4d1e2-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4d1e2-182">Create an Azure AD test user</span></span>

<span data-ttu-id="4d1e2-183">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="4d1e2-185">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1e2-186">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4d1e2-188">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4d1e2-190">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4d1e2-192">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-192">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4d1e2-194">a.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-194">a.</span></span> <span data-ttu-id="4d1e2-195">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d1e2-196">b.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-196">b.</span></span> <span data-ttu-id="4d1e2-197">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4d1e2-198">c.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-198">c.</span></span> <span data-ttu-id="4d1e2-199">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4d1e2-200">d.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-200">d.</span></span> <span data-ttu-id="4d1e2-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="4d1e2-202">Een testgebruiker YouEarnedIt maken</span><span class="sxs-lookup"><span data-stu-id="4d1e2-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="4d1e2-203">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in YouEarnedIt maken.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="4d1e2-204">Neem contact op met het ondersteuningsteam YouEarnedIt de gebruikers van het platform YouEarnedIt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="4d1e2-205">YouEarnedIt verwachten dat de id-Provider op te geven van een EmailAddress of een gebruikersnaam in het kenmerk NameID.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="4d1e2-206">Verificatie mislukt als de overeenkomende gebruikersnaam of EmailAddress niet in de database gevonden is of komt niet exact overeen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="4d1e2-207">Dit vereist dat de accounts worden geïmporteerd in het systeem YouEarnedIt voordat de SSO-integratie (doorgaans op via de API- of CSV-import).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4d1e2-208">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="4d1e2-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="4d1e2-209">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="4d1e2-211">**Britta Simon om aan te wijzen YouEarnedIt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4d1e2-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1e2-212">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4d1e2-214">Selecteer in de lijst met toepassingen **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![De koppeling YouEarnedIt in de lijst met toepassingen](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="4d1e2-216">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-216">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="4d1e2-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-218">Click **Add** button.</span></span> <span data-ttu-id="4d1e2-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="4d1e2-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4d1e2-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d1e2-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4d1e2-224">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4d1e2-224">Test single sign-on</span></span>

<span data-ttu-id="4d1e2-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4d1e2-226">Als u op de tegel YouEarnedIt in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="4d1e2-227">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4d1e2-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4d1e2-228">Additional resources</span></span>

* [<span data-ttu-id="4d1e2-229">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d1e2-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d1e2-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d1e2-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

