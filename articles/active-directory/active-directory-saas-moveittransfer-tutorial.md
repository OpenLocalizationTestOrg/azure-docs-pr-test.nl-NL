---
title: 'Zelfstudie: Azure Active Directory-integratie met MOVEit overdracht - Azure AD-integratie | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en MOVEit overdracht - Azure AD-integratie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="16ed7-103">Zelfstudie: Azure Active Directory-integratie met MOVEit overdracht - Azure AD-integratie</span><span class="sxs-lookup"><span data-stu-id="16ed7-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="16ed7-104">In deze zelfstudie leert u het integreren van MOVEit overdracht - Azure AD-integratie met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16ed7-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16ed7-105">Integratie van MOVEit overdracht - Azure AD-integratie met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="16ed7-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16ed7-106">U kunt beheren in Azure AD die toegang tot MOVEit overdracht - Azure AD-integratie heeft.</span><span class="sxs-lookup"><span data-stu-id="16ed7-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="16ed7-107">U kunt uw gebruikers automatisch ophalen aangemeld bij MOVEit overdracht - Azure AD-integratie met hun Azure AD-accounts (Single Sign-On) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="16ed7-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="16ed7-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="16ed7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="16ed7-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16ed7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16ed7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="16ed7-110">Prerequisites</span></span>

<span data-ttu-id="16ed7-111">Voor het configureren van Azure AD-integratie met MOVEit overdracht - integratie van Azure AD, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="16ed7-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="16ed7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="16ed7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16ed7-113">De overdracht van een MOVEit - Azure AD-integratie eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="16ed7-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16ed7-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="16ed7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16ed7-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="16ed7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16ed7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="16ed7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16ed7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16ed7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16ed7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="16ed7-118">Scenario description</span></span>
<span data-ttu-id="16ed7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="16ed7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16ed7-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="16ed7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16ed7-121">Overdracht van MOVEit - Azure AD-integratie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="16ed7-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="16ed7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="16ed7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="16ed7-123">Overdracht van MOVEit - Azure AD-integratie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="16ed7-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="16ed7-124">Om de integratie van MOVEit overdracht - Azure AD-integratie met Azure AD te configureren die u wilt toevoegen MOVEit overdracht - Azure AD-integratie uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="16ed7-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16ed7-125">**Als u wilt toevoegen MOVEit overdracht - Azure AD-integratie uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="16ed7-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16ed7-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="16ed7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="16ed7-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16ed7-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="16ed7-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16ed7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="16ed7-133">Typ in het zoekvak **MOVEit overdracht - Azure AD-integratie**, selecteer **MOVEit overdracht - Azure AD-integratie** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="16ed7-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![Overdracht van MOVEit - Azure AD-integratie in de lijst met resultaten](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="16ed7-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="16ed7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="16ed7-136">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met MOVEit overdracht - Azure AD-integratie op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="16ed7-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16ed7-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in MOVEit overdracht - Azure AD-integratie is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16ed7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="16ed7-138">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in overdrachts-MOVEit - Azure AD-integratie moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="16ed7-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="16ed7-139">Wijs in overdrachts-MOVEit - Azure AD-integratie, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="16ed7-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="16ed7-140">Als u wilt configureren en testen Azure AD eenmalige aanmelding met MOVEit Transfer - Azure AD-integratie moet u de volgende elementen voltooid:</span><span class="sxs-lookup"><span data-stu-id="16ed7-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16ed7-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16ed7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16ed7-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16ed7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16ed7-143">**[Maken van een overdracht MOVEit - Azure AD-integratie testgebruiker](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - MOVEit overdracht - Azure AD-integratie die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="16ed7-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16ed7-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="16ed7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16ed7-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="16ed7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="16ed7-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="16ed7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="16ed7-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in de overdracht van uw MOVEit - toepassing voor Azure AD-integratie.</span><span class="sxs-lookup"><span data-stu-id="16ed7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="16ed7-148">**Voer de volgende stappen uit voor het configureren van Azure AD eenmalige aanmelding met MOVEit overdracht - Azure AD-integratie:**</span><span class="sxs-lookup"><span data-stu-id="16ed7-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="16ed7-149">In de Azure-portal op de **MOVEit overdracht - Azure AD-integratie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="16ed7-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="16ed7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="16ed7-153">Op de **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="16ed7-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="16ed7-155">a.</span><span class="sxs-lookup"><span data-stu-id="16ed7-155">a.</span></span> <span data-ttu-id="16ed7-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="16ed7-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="16ed7-157">b.</span><span class="sxs-lookup"><span data-stu-id="16ed7-157">b.</span></span> <span data-ttu-id="16ed7-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="16ed7-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="16ed7-159">c.</span><span class="sxs-lookup"><span data-stu-id="16ed7-159">c.</span></span> <span data-ttu-id="16ed7-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="16ed7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="16ed7-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="16ed7-161">These values are not real.</span></span> <span data-ttu-id="16ed7-162">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="16ed7-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="16ed7-163">U kunt deze waarden later in verwijzen **metagegevens-URL voor Service Provider** sectie of neem contact op met [MOVEit overdracht - ondersteuningsteam van Azure AD-integratie Client](https://community.ipswitch.com/s/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="16ed7-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="16ed7-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="16ed7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="16ed7-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="16ed7-166">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="16ed7-168">Meld u aan op uw tenant MOVEit overdracht als beheerder.</span><span class="sxs-lookup"><span data-stu-id="16ed7-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="16ed7-169">Klik in het navigatiedeelvenster links op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-169">On the left navigation pane, click **Settings**.</span></span>

    ![Instellingen sectie op App aan clientzijde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="16ed7-171">Klik op **eenmalige aanmelding** koppeling, die zich onder **beveiligingsbeleid-gebruikersverificatie >**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Security-beleid op App aan clientzijde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="16ed7-173">Klik op de koppeling van de metagegevens-URL voor het downloaden van het metagegevensdocument.</span><span class="sxs-lookup"><span data-stu-id="16ed7-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![Serviceprovider metagegevens-URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="16ed7-175">Controleer of **id van de entiteit** overeenkomt met **id** in de **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie.</span><span class="sxs-lookup"><span data-stu-id="16ed7-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="16ed7-176">Controleer of **AssertionConsumerService** locatie-URL overeenkomt met **antwoord-URL** in de **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie.</span><span class="sxs-lookup"><span data-stu-id="16ed7-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="16ed7-178">Klik op **identiteitsprovider toevoegen** knop een nieuwe federatieve identiteitsprovider toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16ed7-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![ID-Provider toevoegen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="16ed7-180">Klik op **bladeren...**  om te selecteren in het bestand met metagegevens die u hebt gedownload van Azure-portal, klikt u vervolgens op **identiteitsprovider toevoegen** het gedownloade bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="16ed7-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![SAML-identiteitsprovider](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="16ed7-182">Selecteer "**Ja**' als **ingeschakeld** in de **bewerken federatieve identiteit Providerinstellingen...**  pagina en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Federatieve identiteiten Providerinstellingen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="16ed7-184">In de **bewerken federatieve identiteit Provider gebruikersinstellingen** pagina, de volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="16ed7-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![Federatieve identiteiten Providerinstellingen bewerken](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="16ed7-186">a.</span><span class="sxs-lookup"><span data-stu-id="16ed7-186">a.</span></span> <span data-ttu-id="16ed7-187">Selecteer **SAML NameID** als **aanmeldingsnaam**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="16ed7-188">b.</span><span class="sxs-lookup"><span data-stu-id="16ed7-188">b.</span></span> <span data-ttu-id="16ed7-189">Selecteer **andere** als **volledige naam** en in de **kenmerknaam** textbox plaatsen de waarde: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="16ed7-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="16ed7-190">c.</span><span class="sxs-lookup"><span data-stu-id="16ed7-190">c.</span></span> <span data-ttu-id="16ed7-191">Selecteer **andere** als **e** en in de **kenmerknaam** textbox plaatsen de waarde: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="16ed7-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="16ed7-192">d.</span><span class="sxs-lookup"><span data-stu-id="16ed7-192">d.</span></span> <span data-ttu-id="16ed7-193">Selecteer **Ja** als **automatisch maken van account aanmeldt**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="16ed7-194">e.</span><span class="sxs-lookup"><span data-stu-id="16ed7-194">e.</span></span> <span data-ttu-id="16ed7-195">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="16ed7-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="16ed7-196">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="16ed7-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16ed7-197">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="16ed7-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16ed7-198">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16ed7-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="16ed7-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="16ed7-199">Create an Azure AD test user</span></span>

<span data-ttu-id="16ed7-200">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="16ed7-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="16ed7-202">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="16ed7-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16ed7-203">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="16ed7-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="16ed7-205">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="16ed7-207">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16ed7-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="16ed7-209">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="16ed7-209">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="16ed7-211">a.</span><span class="sxs-lookup"><span data-stu-id="16ed7-211">a.</span></span> <span data-ttu-id="16ed7-212">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16ed7-213">b.</span><span class="sxs-lookup"><span data-stu-id="16ed7-213">b.</span></span> <span data-ttu-id="16ed7-214">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16ed7-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="16ed7-215">c.</span><span class="sxs-lookup"><span data-stu-id="16ed7-215">c.</span></span> <span data-ttu-id="16ed7-216">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="16ed7-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="16ed7-217">d.</span><span class="sxs-lookup"><span data-stu-id="16ed7-217">d.</span></span> <span data-ttu-id="16ed7-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="16ed7-219">Een MOVEit Transfer - Azure AD-integratie testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="16ed7-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="16ed7-220">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in MOVEit overdracht - Azure AD-integratie.</span><span class="sxs-lookup"><span data-stu-id="16ed7-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="16ed7-221">Overdracht van MOVEit - Azure AD-integratie ondersteunt just-in-time-inrichting, die u hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="16ed7-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="16ed7-222">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="16ed7-222">There is no action item for you in this section.</span></span> <span data-ttu-id="16ed7-223">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot MOVEit overdracht - Azure AD-integratie als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="16ed7-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="16ed7-224">Als u een gebruiker handmatig maken wilt, moet u contact op met de [MOVEit overdracht - ondersteuningsteam van Azure AD-integratie Client](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="16ed7-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="16ed7-225">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="16ed7-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="16ed7-226">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang op de overdracht van MOVEit - Azure AD-integratie.</span><span class="sxs-lookup"><span data-stu-id="16ed7-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="16ed7-228">**Voer de volgende stappen uit om toe te wijzen Britta Simon op de overdracht van MOVEit - Azure AD-integratie:**</span><span class="sxs-lookup"><span data-stu-id="16ed7-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="16ed7-229">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="16ed7-231">Selecteer in de lijst met toepassingen **MOVEit overdracht - Azure AD-integratie**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![De overdracht MOVEit - Azure AD-integratie koppeling in de lijst met toepassingen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="16ed7-233">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="16ed7-233">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="16ed7-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="16ed7-235">Click **Add** button.</span></span> <span data-ttu-id="16ed7-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16ed7-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="16ed7-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="16ed7-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16ed7-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16ed7-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16ed7-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="16ed7-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="16ed7-241">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="16ed7-241">Test single sign-on</span></span>

<span data-ttu-id="16ed7-242">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="16ed7-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="16ed7-243">Wanneer u klikt op de overdracht MOVEit - tegel Azure AD-integratie in het deelvenster toegang u moet ophalen automatisch aangemeld bij de overdracht van uw MOVEit - toepassing voor Azure AD-integratie.</span><span class="sxs-lookup"><span data-stu-id="16ed7-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="16ed7-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="16ed7-244">Additional resources</span></span>

* [<span data-ttu-id="16ed7-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16ed7-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16ed7-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="16ed7-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

