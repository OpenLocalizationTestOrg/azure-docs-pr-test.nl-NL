---
title: 'Zelfstudie: Azure Active Directory-integratie met AirWatch | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="c37f1-103">Zelfstudie: Azure Active Directory-integratie met AirWatch</span><span class="sxs-lookup"><span data-stu-id="c37f1-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="c37f1-104">In deze zelfstudie leert u hoe AirWatch integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c37f1-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c37f1-105">AirWatch integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c37f1-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c37f1-106">U kunt beheren in Azure AD die toegang tot AirWatch heeft</span><span class="sxs-lookup"><span data-stu-id="c37f1-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="c37f1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij AirWatch (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c37f1-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c37f1-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c37f1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c37f1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c37f1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c37f1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c37f1-110">Prerequisites</span></span>

<span data-ttu-id="c37f1-111">Voor het configureren van Azure AD-integratie met AirWatch, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c37f1-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="c37f1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c37f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c37f1-113">Een AirWatch eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c37f1-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c37f1-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c37f1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c37f1-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c37f1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c37f1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c37f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c37f1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c37f1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c37f1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c37f1-118">Scenario description</span></span>
<span data-ttu-id="c37f1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c37f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c37f1-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c37f1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c37f1-121">AirWatch uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c37f1-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="c37f1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c37f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="c37f1-123">AirWatch uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c37f1-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="c37f1-124">Voor het configureren van de integratie van AirWatch in Azure AD, moet u AirWatch uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c37f1-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c37f1-125">**Als u wilt toevoegen AirWatch uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c37f1-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c37f1-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c37f1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c37f1-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c37f1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c37f1-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c37f1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c37f1-133">Typ in het zoekvak **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-133">In the search box, type **AirWatch**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="c37f1-135">Selecteer in het deelvenster resultaten **AirWatch**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c37f1-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c37f1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c37f1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c37f1-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met AirWatch op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c37f1-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c37f1-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in AirWatch is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c37f1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="c37f1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in AirWatch tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="c37f1-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="c37f1-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in AirWatch.</span><span class="sxs-lookup"><span data-stu-id="c37f1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="c37f1-142">Om te configureren en testen van Azure AD eenmalige aanmelding met AirWatch, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c37f1-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c37f1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c37f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c37f1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c37f1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c37f1-145">**[Maken van een testgebruiker AirWatch](#creating-a-airwatch-test-user)**  - AirWatch die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="c37f1-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c37f1-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c37f1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c37f1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c37f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c37f1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c37f1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c37f1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing AirWatch configureren.</span><span class="sxs-lookup"><span data-stu-id="c37f1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="c37f1-150">**Voor het configureren van Azure AD eenmalige aanmelding met AirWatch, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c37f1-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="c37f1-151">In de Azure-portal op de **AirWatch** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c37f1-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c37f1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="c37f1-155">Op de **AirWatch domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c37f1-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="c37f1-157">a.</span><span class="sxs-lookup"><span data-stu-id="c37f1-157">a.</span></span> <span data-ttu-id="c37f1-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="c37f1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="c37f1-159">b.</span><span class="sxs-lookup"><span data-stu-id="c37f1-159">b.</span></span> <span data-ttu-id="c37f1-160">In de **id** textbox, typ de waarde als`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="c37f1-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c37f1-161">Deze waarde is niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="c37f1-161">This value is not the real.</span></span> <span data-ttu-id="c37f1-162">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c37f1-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="c37f1-163">Neem contact op met [AirWatch Client ondersteuningsteam](http://www.air-watch.com/company/contact-us/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="c37f1-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="c37f1-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c37f1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="c37f1-166">Op de **AirWatch configuratie** sectie, klikt u op **configureren AirWatch** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c37f1-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c37f1-167">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c37f1-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="c37f1-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c37f1-169">Click **Save** button.</span></span>

    <span data-ttu-id="c37f1-170">![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="c37f1-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="c37f1-171">In een ander browservenster, meld u aan bij uw bedrijf AirWatch site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c37f1-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="c37f1-172">Klik in het navigatiedeelvenster links op **Accounts**, en klik vervolgens op **beheerders**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="c37f1-173">![Beheerders](./media/active-directory-saas-airwatch-tutorial/ic791920.png "beheerders")</span><span class="sxs-lookup"><span data-stu-id="c37f1-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="c37f1-174">Vouw de **instellingen** menu en klik vervolgens op **Directory Services**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="c37f1-175">![Instellingen](./media/active-directory-saas-airwatch-tutorial/ic791921.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="c37f1-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="c37f1-176">Klik op de **gebruiker** tabblad, in de **Base DN** textbox, typ de naam van uw domein en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="c37f1-177">![Gebruiker](./media/active-directory-saas-airwatch-tutorial/ic791922.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="c37f1-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="c37f1-178">Klik op de **Server** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c37f1-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="c37f1-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span><span class="sxs-lookup"><span data-stu-id="c37f1-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="c37f1-180">De volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c37f1-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="c37f1-181">![Uploaden](./media/active-directory-saas-airwatch-tutorial/ic791924.png "uploaden")</span><span class="sxs-lookup"><span data-stu-id="c37f1-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="c37f1-182">a.</span><span class="sxs-lookup"><span data-stu-id="c37f1-182">a.</span></span> <span data-ttu-id="c37f1-183">Als **maptype**, selecteer **geen**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="c37f1-184">b.</span><span class="sxs-lookup"><span data-stu-id="c37f1-184">b.</span></span> <span data-ttu-id="c37f1-185">Selecteer **SAML gebruiken voor verificatie**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="c37f1-186">c.</span><span class="sxs-lookup"><span data-stu-id="c37f1-186">c.</span></span> <span data-ttu-id="c37f1-187">De gedownloade om certificaat te uploaden, klikt u op **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="c37f1-188">In de **aanvragen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c37f1-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="c37f1-189">![Aanvraag](./media/active-directory-saas-airwatch-tutorial/ic791925.png "aanvragen")</span><span class="sxs-lookup"><span data-stu-id="c37f1-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="c37f1-190">a.</span><span class="sxs-lookup"><span data-stu-id="c37f1-190">a.</span></span> <span data-ttu-id="c37f1-191">Als **Binding aanvraagtype**, selecteer **POST**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="c37f1-192">b.</span><span class="sxs-lookup"><span data-stu-id="c37f1-192">b.</span></span> <span data-ttu-id="c37f1-193">In de Azure-portal op de **op Airwatch eenmalige aanmelding configureren** dialoogvenster pagina-, Kopieer de **SAML Single Sign-On Service-URL** waarde en plak deze in de **identiteit Provider eenmalige aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c37f1-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="c37f1-194">c.</span><span class="sxs-lookup"><span data-stu-id="c37f1-194">c.</span></span> <span data-ttu-id="c37f1-195">Als **NameID indeling**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="c37f1-196">d.</span><span class="sxs-lookup"><span data-stu-id="c37f1-196">d.</span></span> <span data-ttu-id="c37f1-197">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-197">Click **Save**.</span></span>

14. <span data-ttu-id="c37f1-198">Klik op de **gebruiker** tabblad opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c37f1-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="c37f1-199">![Gebruiker](./media/active-directory-saas-airwatch-tutorial/ic791926.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="c37f1-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="c37f1-200">In de **kenmerk** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c37f1-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="c37f1-201">![Kenmerk](./media/active-directory-saas-airwatch-tutorial/ic791927.png "kenmerk")</span><span class="sxs-lookup"><span data-stu-id="c37f1-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="c37f1-202">a.</span><span class="sxs-lookup"><span data-stu-id="c37f1-202">a.</span></span> <span data-ttu-id="c37f1-203">In de **Object-id** textbox type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="c37f1-204">b.</span><span class="sxs-lookup"><span data-stu-id="c37f1-204">b.</span></span> <span data-ttu-id="c37f1-205">In de **gebruikersnaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="c37f1-206">c.</span><span class="sxs-lookup"><span data-stu-id="c37f1-206">c.</span></span> <span data-ttu-id="c37f1-207">In de **weergavenaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="c37f1-208">d.</span><span class="sxs-lookup"><span data-stu-id="c37f1-208">d.</span></span> <span data-ttu-id="c37f1-209">In de **voornaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="c37f1-210">e.</span><span class="sxs-lookup"><span data-stu-id="c37f1-210">e.</span></span> <span data-ttu-id="c37f1-211">In de **achternaam** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="c37f1-212">f.</span><span class="sxs-lookup"><span data-stu-id="c37f1-212">f.</span></span> <span data-ttu-id="c37f1-213">In de **e** textbox type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="c37f1-214">g.</span><span class="sxs-lookup"><span data-stu-id="c37f1-214">g.</span></span> <span data-ttu-id="c37f1-215">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c37f1-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c37f1-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="c37f1-217">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c37f1-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c37f1-219">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c37f1-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c37f1-220">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c37f1-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c37f1-222">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c37f1-224">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c37f1-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c37f1-226">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c37f1-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c37f1-228">a.</span><span class="sxs-lookup"><span data-stu-id="c37f1-228">a.</span></span> <span data-ttu-id="c37f1-229">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c37f1-230">b.</span><span class="sxs-lookup"><span data-stu-id="c37f1-230">b.</span></span> <span data-ttu-id="c37f1-231">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c37f1-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c37f1-232">c.</span><span class="sxs-lookup"><span data-stu-id="c37f1-232">c.</span></span> <span data-ttu-id="c37f1-233">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c37f1-234">d.</span><span class="sxs-lookup"><span data-stu-id="c37f1-234">d.</span></span> <span data-ttu-id="c37f1-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="c37f1-236">Een testgebruiker AirWatch maken</span><span class="sxs-lookup"><span data-stu-id="c37f1-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="c37f1-237">Om Azure AD-gebruikers zich aanmelden bij AirWatch, moeten ze worden ingericht op AirWatch.</span><span class="sxs-lookup"><span data-stu-id="c37f1-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="c37f1-238">AirWatch, inrichting wanneer een handmatige taak is.</span><span class="sxs-lookup"><span data-stu-id="c37f1-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="c37f1-239">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c37f1-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c37f1-240">Meld u aan bij uw **AirWatch** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="c37f1-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="c37f1-241">Klik in het navigatievenster aan de linkerkant op **Accounts**, en klik vervolgens op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="c37f1-242">![Gebruikers](./media/active-directory-saas-airwatch-tutorial/ic791929.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="c37f1-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="c37f1-243">In de **gebruikers** menu, klikt u op **lijstweergave**, en klik vervolgens op **toevoegen \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="c37f1-244">![Gebruiker toevoegen](./media/active-directory-saas-airwatch-tutorial/ic791930.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="c37f1-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="c37f1-245">Op de **toevoegen / bewerken van de gebruiker** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c37f1-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="c37f1-246">![Gebruiker toevoegen](./media/active-directory-saas-airwatch-tutorial/ic791931.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="c37f1-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="c37f1-247">Typ de **gebruikersnaam**, **wachtwoord**, **wachtwoord bevestigen**, **voornaam**, **achternaam**, **e-mailadres** van een geldige Azure Active Directory-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="c37f1-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="c37f1-248">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c37f1-249">U kunt andere AirWatch gebruiker account hulpmiddelen voor het maken of API's die is geleverd door AirWatch aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c37f1-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c37f1-250">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c37f1-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c37f1-251">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan AirWatch.</span><span class="sxs-lookup"><span data-stu-id="c37f1-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c37f1-253">**Britta Simon om aan te wijzen AirWatch, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c37f1-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="c37f1-254">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c37f1-256">Selecteer in de lijst met toepassingen **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-256">In the applications list, select **AirWatch**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="c37f1-258">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c37f1-258">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c37f1-260">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c37f1-260">Click **Add** button.</span></span> <span data-ttu-id="c37f1-261">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c37f1-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c37f1-263">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c37f1-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c37f1-264">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c37f1-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c37f1-265">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c37f1-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c37f1-266">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c37f1-266">Testing single sign-on</span></span>

<span data-ttu-id="c37f1-267">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c37f1-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c37f1-268">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c37f1-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c37f1-269">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c37f1-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c37f1-270">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c37f1-270">Additional resources</span></span>

* [<span data-ttu-id="c37f1-271">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c37f1-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c37f1-272">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c37f1-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

