---
title: 'Zelfstudie: Azure Active Directory-integratie met Neota logica Studio | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Neota logica Studio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 99018277392cab44a6b579ad45b4611739a803d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="749b2-103">Zelfstudie: Azure Active Directory-integratie met Neota logica Studio</span><span class="sxs-lookup"><span data-stu-id="749b2-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="749b2-104">In deze zelfstudie leert u hoe Neota logica Studio integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="749b2-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="749b2-105">Neota logica Studio integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="749b2-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="749b2-106">U kunt beheren in Azure AD die toegang tot Neota logica Studio heeft</span><span class="sxs-lookup"><span data-stu-id="749b2-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="749b2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Neota logica Studio (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="749b2-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="749b2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="749b2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="749b2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, zien.</span><span class="sxs-lookup"><span data-stu-id="749b2-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="749b2-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="749b2-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="749b2-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="749b2-111">Prerequisites</span></span>

<span data-ttu-id="749b2-112">Voor het configureren van Azure AD-integratie met Neota logica Studio, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="749b2-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="749b2-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="749b2-113">An Azure AD subscription</span></span>
- <span data-ttu-id="749b2-114">Een Neota logica Studio eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="749b2-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="749b2-115">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="749b2-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="749b2-116">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="749b2-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="749b2-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="749b2-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="749b2-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="749b2-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="749b2-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="749b2-119">Scenario description</span></span>

<span data-ttu-id="749b2-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="749b2-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="749b2-121">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="749b2-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="749b2-122">Neota logica Studio uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="749b2-122">Adding Neota Logic Studio from the gallery</span></span>
2. <span data-ttu-id="749b2-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="749b2-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="749b2-124">Neota logica Studio uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="749b2-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="749b2-125">Voor het configureren van de integratie van Neota logica Studio in Azure AD, moet u Neota logica Studio uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="749b2-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="749b2-126">**Als u wilt toevoegen Neota logica Studio uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="749b2-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="749b2-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="749b2-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="749b2-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="749b2-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="749b2-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="749b2-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="749b2-132">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="749b2-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="749b2-134">Typ in het zoekvak **Neota logica Studio**.</span><span class="sxs-lookup"><span data-stu-id="749b2-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="749b2-136">Selecteer in het deelvenster resultaten **Neota logica Studio**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="749b2-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="749b2-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="749b2-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="749b2-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Neota logica Studio op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="749b2-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="749b2-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Neota logica Studio is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="749b2-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="749b2-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Neota logica Studio tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="749b2-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="749b2-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Neota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="749b2-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="749b2-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Neota logica Studio, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="749b2-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="749b2-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="749b2-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="749b2-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="749b2-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="749b2-146">**[Maken van een testgebruiker Neota logica Studio](#creating-a-neota-logic-studio-test-user)**  - Neota logica Studio die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="749b2-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="749b2-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="749b2-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="749b2-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="749b2-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="749b2-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="749b2-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="749b2-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Neota logica Studio configureren.</span><span class="sxs-lookup"><span data-stu-id="749b2-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="749b2-151">**Voor het configureren van Azure AD eenmalige aanmelding met Neota logica Studio, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="749b2-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="749b2-152">In de Azure-portal op de **Neota logica Studio** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="749b2-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="749b2-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="749b2-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="749b2-156">Op de **Neota logica Studio domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="749b2-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="749b2-158">a.</span><span class="sxs-lookup"><span data-stu-id="749b2-158">a.</span></span> <span data-ttu-id="749b2-159">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="749b2-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="749b2-160">b.</span><span class="sxs-lookup"><span data-stu-id="749b2-160">b.</span></span> <span data-ttu-id="749b2-161">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="749b2-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="749b2-162">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="749b2-162">These values are not the real.</span></span> <span data-ttu-id="749b2-163">Deze waarden bijwerken met de werkelijke aanmeldings-URL & -id.</span><span class="sxs-lookup"><span data-stu-id="749b2-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="749b2-164">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="749b2-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="749b2-165">Neem contact op met [Neota logica Studio Client ondersteuningsteam](https://www.neotalogic.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="749b2-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="749b2-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="749b2-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="749b2-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="749b2-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="749b2-170">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [Neota logica Studio ondersteuning](https://www.neotalogic.com/contact-us/) team en bieden ze gedownload met **Metadata XML** bestand.</span><span class="sxs-lookup"><span data-stu-id="749b2-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="749b2-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="749b2-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="749b2-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="749b2-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="749b2-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="749b2-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="749b2-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="749b2-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="749b2-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="749b2-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="749b2-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="749b2-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="749b2-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="749b2-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="749b2-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="749b2-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="749b2-182">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="749b2-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="749b2-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="749b2-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="749b2-186">a.</span><span class="sxs-lookup"><span data-stu-id="749b2-186">a.</span></span> <span data-ttu-id="749b2-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="749b2-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="749b2-188">b.</span><span class="sxs-lookup"><span data-stu-id="749b2-188">b.</span></span> <span data-ttu-id="749b2-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="749b2-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="749b2-190">c.</span><span class="sxs-lookup"><span data-stu-id="749b2-190">c.</span></span> <span data-ttu-id="749b2-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="749b2-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="749b2-192">d.</span><span class="sxs-lookup"><span data-stu-id="749b2-192">d.</span></span> <span data-ttu-id="749b2-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="749b2-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="749b2-194">Een testgebruiker Neota logica Studio maken</span><span class="sxs-lookup"><span data-stu-id="749b2-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="749b2-195">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Neota logica Studio maken.</span><span class="sxs-lookup"><span data-stu-id="749b2-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="749b2-196">werken met [Neota logica Studio Client ondersteuningsteam](https://www.neotalogic.com/contact-us/) om toe te voegen de gebruikers van het platform Neota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="749b2-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="749b2-197">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="749b2-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="749b2-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="749b2-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="749b2-199">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Neota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="749b2-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="749b2-201">**Britta Simon om aan te wijzen Neota logica Studio, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="749b2-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="749b2-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="749b2-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="749b2-204">Selecteer in de lijst met toepassingen **Neota logica Studio**.</span><span class="sxs-lookup"><span data-stu-id="749b2-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="749b2-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="749b2-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="749b2-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="749b2-208">Click **Add** button.</span></span> <span data-ttu-id="749b2-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="749b2-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="749b2-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="749b2-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="749b2-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="749b2-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="749b2-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="749b2-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="749b2-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="749b2-214">Testing single sign-on</span></span>

<span data-ttu-id="749b2-215">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="749b2-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="749b2-216">Klik op de tegel Neota logica Studio in het deelvenster toegang, wordt u omgeleid naar de organisatie aanmelding pagina.</span><span class="sxs-lookup"><span data-stu-id="749b2-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="749b2-217">Na een geslaagde aanmelding u zal worden aangemeld bij uw toepassing Neota logica Studio.</span><span class="sxs-lookup"><span data-stu-id="749b2-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="749b2-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="749b2-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="749b2-219">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="749b2-219">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="749b2-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="749b2-220">Additional resources</span></span>

* [<span data-ttu-id="749b2-221">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="749b2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="749b2-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="749b2-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

