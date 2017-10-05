---
title: 'Zelfstudie: Azure Active Directory-integratie met Evidence.com | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Evidence.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="8165b-103">Zelfstudie: Azure Active Directory-integratie met Evidence.com</span><span class="sxs-lookup"><span data-stu-id="8165b-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="8165b-104">In deze zelfstudie leert u hoe Evidence.com integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8165b-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8165b-105">Evidence.com integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8165b-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8165b-106">U kunt beheren in Azure AD die toegang tot Evidence.com heeft.</span><span class="sxs-lookup"><span data-stu-id="8165b-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="8165b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Evidence.com (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8165b-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8165b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="8165b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8165b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8165b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8165b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8165b-110">Prerequisites</span></span>

<span data-ttu-id="8165b-111">Voor het configureren van Azure AD-integratie met Evidence.com, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="8165b-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="8165b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8165b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8165b-113">Een Evidence.com eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8165b-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8165b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8165b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8165b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8165b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8165b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8165b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8165b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8165b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8165b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8165b-118">Scenario description</span></span>
<span data-ttu-id="8165b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8165b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8165b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8165b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8165b-121">Evidence.com uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8165b-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="8165b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8165b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="8165b-123">Evidence.com uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8165b-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="8165b-124">Voor het configureren van de integratie van Evidence.com in Azure AD, moet u Evidence.com uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8165b-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8165b-125">**Als u wilt toevoegen Evidence.com uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8165b-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8165b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8165b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="8165b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8165b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8165b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8165b-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="8165b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8165b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="8165b-133">Typ in het zoekvak **Evidence.com**, selecteer **Evidence.com** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8165b-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![Evidence.com in de lijst met resultaten](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8165b-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="8165b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8165b-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Evidence.com op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="8165b-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8165b-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Evidence.com is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8165b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="8165b-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Evidence.com tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="8165b-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="8165b-139">Wijs in Evidence.com, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="8165b-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8165b-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Evidence.com, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="8165b-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8165b-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8165b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8165b-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8165b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8165b-143">**[Maak een testgebruiker Evidence.com](#create-a-evidencecom-test-user)**  - Evidence.com die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="8165b-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8165b-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8165b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8165b-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8165b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8165b-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8165b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8165b-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Evidence.com configureren.</span><span class="sxs-lookup"><span data-stu-id="8165b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="8165b-148">**Voor het configureren van Azure AD eenmalige aanmelding met Evidence.com, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8165b-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="8165b-149">In de Azure-portal op de **Evidence.com** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8165b-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8165b-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8165b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="8165b-153">Op de **Evidence.com domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8165b-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en evidence.com domein eenmalige aanmelding informatie](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="8165b-155">a.</span><span class="sxs-lookup"><span data-stu-id="8165b-155">a.</span></span> <span data-ttu-id="8165b-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="8165b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="8165b-157">b.</span><span class="sxs-lookup"><span data-stu-id="8165b-157">b.</span></span> <span data-ttu-id="8165b-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="8165b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8165b-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="8165b-159">These values are not real.</span></span> <span data-ttu-id="8165b-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="8165b-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8165b-161">Neem contact op met [Evidence.com Client ondersteuningsteam](https://communities.taser.com/support/SupportContactUs?typ=LE) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8165b-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="8165b-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8165b-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="8165b-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8165b-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8165b-166">Op de **Evidence.com configuratie** sectie, klikt u op **configureren Evidence.com** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="8165b-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8165b-167">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="8165b-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evidence.com configuratie](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="8165b-169">In een afzonderlijke browservenster, meld u aan bij uw Evidence.com tenant als beheerder en navigeer naar **Admin** tabblad</span><span class="sxs-lookup"><span data-stu-id="8165b-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="8165b-170">Klik op **Agency voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="8165b-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="8165b-171">Selecteer **SAML eenmalige aanmelding op basis van**</span><span class="sxs-lookup"><span data-stu-id="8165b-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="8165b-172">Kopieer de **SAML entiteit-ID**, **SAML Single Sign-On Service-URL** en **Sign-Out URL** waarden die worden weergegeven in de Azure-portal en de overeenkomende velden in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="8165b-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="8165b-173">Open uw gedownloade Certificate(Base64)-bestand in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **beveiligingscertificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="8165b-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="8165b-174">Sla de configuratie in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="8165b-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="8165b-175">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="8165b-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8165b-176">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="8165b-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8165b-177">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8165b-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8165b-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8165b-178">Create an Azure AD test user</span></span>

<span data-ttu-id="8165b-179">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8165b-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="8165b-181">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8165b-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8165b-182">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="8165b-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8165b-184">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8165b-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8165b-186">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8165b-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8165b-188">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8165b-188">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8165b-190">a.</span><span class="sxs-lookup"><span data-stu-id="8165b-190">a.</span></span> <span data-ttu-id="8165b-191">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8165b-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8165b-192">b.</span><span class="sxs-lookup"><span data-stu-id="8165b-192">b.</span></span> <span data-ttu-id="8165b-193">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8165b-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8165b-194">c.</span><span class="sxs-lookup"><span data-stu-id="8165b-194">c.</span></span> <span data-ttu-id="8165b-195">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="8165b-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8165b-196">d.</span><span class="sxs-lookup"><span data-stu-id="8165b-196">d.</span></span> <span data-ttu-id="8165b-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8165b-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="8165b-198">Een testgebruiker Evidence.com maken</span><span class="sxs-lookup"><span data-stu-id="8165b-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="8165b-199">Azure AD-gebruikers moeten kunnen aanmelden, als ze worden ingericht om toegang te krijgen in de toepassing Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="8165b-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="8165b-200">Deze sectie wordt beschreven hoe u Azure AD-gebruikersaccounts in Evidence.com maken</span><span class="sxs-lookup"><span data-stu-id="8165b-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="8165b-201">**Voor het inrichten van een gebruikersaccount in Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="8165b-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="8165b-202">In een browservenster geopend, meld u bij uw bedrijf Evidence.com site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8165b-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="8165b-203">Navigeer naar **Admin** tabblad.</span><span class="sxs-lookup"><span data-stu-id="8165b-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="8165b-204">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8165b-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="8165b-205">Klik op de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8165b-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="8165b-206">De **e-mailadres** van de toegevoegde gebruiker moet overeenkomen met de gebruikersnaam van de gebruikers in Azure AD die u wilt toegang geven.</span><span class="sxs-lookup"><span data-stu-id="8165b-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="8165b-207">Als de gebruikersnaam en e-mailadres niet dezelfde waarde in uw organisatie, kunt u de **Evidence.com > kenmerken > eenmalige aanmelding** sectie van de Azure portal om te wijzigen van de nameidenitifer naar Evidence.com verzonden om te worden de e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="8165b-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8165b-208">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="8165b-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="8165b-209">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="8165b-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="8165b-211">**Britta Simon om aan te wijzen Evidence.com, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8165b-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="8165b-212">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8165b-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8165b-214">Selecteer in de lijst met toepassingen **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="8165b-214">In the applications list, select **Evidence.com**.</span></span>

    ![De koppeling Evidence.com in de lijst met toepassingen](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="8165b-216">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8165b-216">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="8165b-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8165b-218">Click **Add** button.</span></span> <span data-ttu-id="8165b-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8165b-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="8165b-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8165b-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8165b-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8165b-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8165b-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8165b-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8165b-224">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8165b-224">Test single sign-on</span></span>

<span data-ttu-id="8165b-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8165b-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8165b-226">Als u op de tegel Evidence.com in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="8165b-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="8165b-227">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8165b-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8165b-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8165b-228">Additional resources</span></span>

* [<span data-ttu-id="8165b-229">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8165b-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8165b-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8165b-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

