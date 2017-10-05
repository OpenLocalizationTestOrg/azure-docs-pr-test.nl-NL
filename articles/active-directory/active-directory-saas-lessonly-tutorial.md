---
title: 'Zelfstudie: Azure Active Directory-integratie met Lesson.ly | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Lesson.ly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fc1e1b2de0a138dbe88d794f802b002321948ab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="ad13e-103">Zelfstudie: Azure Active Directory-integratie met Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="ad13e-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="ad13e-104">In deze zelfstudie leert u hoe Lesson.ly integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad13e-104">In this tutorial, you learn how to integrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad13e-105">Lesson.ly integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ad13e-105">Integrating Lesson.ly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ad13e-106">U kunt beheren in Azure AD die toegang tot Lesson.ly heeft</span><span class="sxs-lookup"><span data-stu-id="ad13e-106">You can control in Azure AD who has access to Lesson.ly</span></span>
- <span data-ttu-id="ad13e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Lesson.ly (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ad13e-107">You can enable your users to automatically get signed-on to Lesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad13e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ad13e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ad13e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad13e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad13e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ad13e-110">Prerequisites</span></span>

<span data-ttu-id="ad13e-111">Voor het configureren van Azure AD-integratie met Lesson.ly, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ad13e-111">To configure Azure AD integration with Lesson.ly, you need the following items:</span></span>

- <span data-ttu-id="ad13e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ad13e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad13e-113">Een Lesson.ly eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ad13e-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad13e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad13e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad13e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ad13e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad13e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ad13e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad13e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad13e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad13e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ad13e-118">Scenario description</span></span>
<span data-ttu-id="ad13e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ad13e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad13e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ad13e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad13e-121">Lesson.ly uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ad13e-121">Adding Lesson.ly from the gallery</span></span>
2. <span data-ttu-id="ad13e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad13e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-the-gallery"></a><span data-ttu-id="ad13e-123">Lesson.ly uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ad13e-123">Adding Lesson.ly from the gallery</span></span>
<span data-ttu-id="ad13e-124">Voor het configureren van de integratie van Lesson.ly in Azure AD, moet u Lesson.ly uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ad13e-124">To configure the integration of Lesson.ly into Azure AD, you need to add Lesson.ly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ad13e-125">**Als u wilt toevoegen Lesson.ly uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ad13e-125">**To add Lesson.ly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ad13e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad13e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad13e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ad13e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ad13e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ad13e-133">Typ in het zoekvak **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-133">In the search box, type **Lesson.ly**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="ad13e-135">Selecteer in het deelvenster resultaten **Lesson.ly**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad13e-135">In the results panel, select **Lesson.ly**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad13e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad13e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad13e-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Lesson.ly op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ad13e-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad13e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Lesson.ly is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad13e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lesson.ly is to a user in Azure AD.</span></span> <span data-ttu-id="ad13e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Lesson.ly tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ad13e-140">In other words, a link relationship between an Azure AD user and the related user in Lesson.ly needs to be established.</span></span>

<span data-ttu-id="ad13e-141">Wijs in Lesson.ly, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ad13e-141">In Lesson.ly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ad13e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Lesson.ly, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ad13e-142">To configure and test Azure AD single sign-on with Lesson.ly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ad13e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad13e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ad13e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad13e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad13e-145">**[Maken van een testgebruiker Lesson.ly](#creating-a-lessonly-test-user)**  - Lesson.ly die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ad13e-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - to have a counterpart of Britta Simon in Lesson.ly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad13e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ad13e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad13e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ad13e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad13e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ad13e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad13e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Lesson.ly configureren.</span><span class="sxs-lookup"><span data-stu-id="ad13e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="ad13e-150">**Voor het configureren van Azure AD eenmalige aanmelding met Lesson.ly, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ad13e-150">**To configure Azure AD single sign-on with Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="ad13e-151">In de Azure-portal op de **Lesson.ly** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-151">In the Azure portal, on the **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ad13e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ad13e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="ad13e-155">Op de **Lesson.ly domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ad13e-155">On the **Lesson.ly Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="ad13e-157">a.</span><span class="sxs-lookup"><span data-stu-id="ad13e-157">a.</span></span> <span data-ttu-id="ad13e-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ad13e-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="ad13e-159">Wanneer een algemeen verwijst naar een naam die **NaamBedrijf** moet worden vervangen door feitelijke naam.</span><span class="sxs-lookup"><span data-stu-id="ad13e-159">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>
    
    <span data-ttu-id="ad13e-160">b.</span><span class="sxs-lookup"><span data-stu-id="ad13e-160">b.</span></span> <span data-ttu-id="ad13e-161">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="ad13e-161">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="ad13e-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ad13e-162">These values are not real.</span></span> <span data-ttu-id="ad13e-163">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="ad13e-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ad13e-164">Neem contact op met [Lesson.ly Client ondersteuningsteam](mailto:dev@lessonly.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ad13e-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) to get these values.</span></span> 

4. <span data-ttu-id="ad13e-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ad13e-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="ad13e-167">De toepassing Lesson.ly verwacht de SAML-asserties in een specifieke indeling waarvoor u het toevoegen van aangepast kenmerktoewijzingen aan uw **SAML-Token kenmerken** configuratie. De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="ad13e-167">The Lesson.ly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="ad13e-169">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ad13e-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="ad13e-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ad13e-170">Attribute Name</span></span>   | <span data-ttu-id="ad13e-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ad13e-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="ad13e-172">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="ad13e-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="ad13e-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ad13e-173">user.givenname</span></span> |
    | <span data-ttu-id="ad13e-174">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="ad13e-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="ad13e-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="ad13e-175">user.surname</span></span> |
    | <span data-ttu-id="ad13e-176">urn: oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="ad13e-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="ad13e-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="ad13e-177">user.mail</span></span> |

    <span data-ttu-id="ad13e-178">a.</span><span class="sxs-lookup"><span data-stu-id="ad13e-178">a.</span></span> <span data-ttu-id="ad13e-179">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ad13e-182">b.</span><span class="sxs-lookup"><span data-stu-id="ad13e-182">b.</span></span> <span data-ttu-id="ad13e-183">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ad13e-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ad13e-184">c.</span><span class="sxs-lookup"><span data-stu-id="ad13e-184">c.</span></span> <span data-ttu-id="ad13e-185">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ad13e-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ad13e-186">d.</span><span class="sxs-lookup"><span data-stu-id="ad13e-186">d.</span></span> <span data-ttu-id="ad13e-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="ad13e-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ad13e-188">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ad13e-190">Op de **Lesson.ly configuratie** sectie, klikt u op **configureren Lesson.ly** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-190">On the **Lesson.ly Configuration** section, click **Configure Lesson.ly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ad13e-191">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ad13e-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="ad13e-193">Eenmalige aanmelding configureren op **Lesson.ly** zijde, moet u de gedownloade verzenden **Certificate(Base64)** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**naar [Lesson.ly ondersteuningsteam](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="ad13e-193">To configure single sign-on on **Lesson.ly** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="ad13e-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ad13e-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ad13e-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ad13e-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ad13e-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad13e-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad13e-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ad13e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad13e-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ad13e-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ad13e-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ad13e-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ad13e-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ad13e-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad13e-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad13e-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad13e-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ad13e-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad13e-209">a.</span><span class="sxs-lookup"><span data-stu-id="ad13e-209">a.</span></span> <span data-ttu-id="ad13e-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad13e-211">b.</span><span class="sxs-lookup"><span data-stu-id="ad13e-211">b.</span></span> <span data-ttu-id="ad13e-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad13e-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad13e-213">c.</span><span class="sxs-lookup"><span data-stu-id="ad13e-213">c.</span></span> <span data-ttu-id="ad13e-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ad13e-215">d.</span><span class="sxs-lookup"><span data-stu-id="ad13e-215">d.</span></span> <span data-ttu-id="ad13e-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="ad13e-217">Een testgebruiker Lesson.ly maken</span><span class="sxs-lookup"><span data-stu-id="ad13e-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="ad13e-218">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Lesson.ly genoemd.</span><span class="sxs-lookup"><span data-stu-id="ad13e-218">The objective of this section is to create a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="ad13e-219">Lesson.LY ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ad13e-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ad13e-220">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="ad13e-220">There is no action item for you in this section.</span></span> <span data-ttu-id="ad13e-221">Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot Lesson.ly als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="ad13e-221">A new user will be created during an attempt to access Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="ad13e-222">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Lesson.ly ondersteuningsteam](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="ad13e-222">If you need to create an user manually, you need to contact the [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ad13e-223">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad13e-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ad13e-224">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="ad13e-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lesson.ly.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ad13e-226">**Britta Simon om aan te wijzen Lesson.ly, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ad13e-226">**To assign Britta Simon to Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="ad13e-227">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ad13e-229">Selecteer in de lijst met toepassingen **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-229">In the applications list, select **Lesson.ly**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="ad13e-231">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ad13e-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ad13e-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ad13e-233">Click **Add** button.</span></span> <span data-ttu-id="ad13e-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ad13e-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ad13e-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ad13e-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad13e-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad13e-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ad13e-239">Testing single sign-on</span></span>

<span data-ttu-id="ad13e-240">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="ad13e-240">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ad13e-241">Als u op de tegel Lesson.ly in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="ad13e-241">When you click the Lesson.ly tile in the Access Panel, you should get automatically signed-on to your Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad13e-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad13e-242">Additional resources</span></span>

* [<span data-ttu-id="ad13e-243">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad13e-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad13e-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad13e-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

