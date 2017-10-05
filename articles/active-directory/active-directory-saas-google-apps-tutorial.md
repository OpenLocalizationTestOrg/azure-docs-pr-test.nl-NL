---
title: 'Zelfstudie: Azure Active Directory-integratie met Google Apps in Azure | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Google Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="a1a20-103">Zelfstudie: Azure Active Directory-integratie met Google Apps</span><span class="sxs-lookup"><span data-stu-id="a1a20-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="a1a20-104">In deze zelfstudie leert u hoe Google Apps integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1a20-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1a20-105">Google Apps integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a1a20-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a1a20-106">U kunt beheren in Azure AD die toegang tot de Google Apps heeft</span><span class="sxs-lookup"><span data-stu-id="a1a20-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="a1a20-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Google Apps (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="a1a20-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1a20-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a1a20-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a1a20-109">Als u meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1a20-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1a20-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a1a20-110">Prerequisites</span></span>

<span data-ttu-id="a1a20-111">Voor het configureren van Azure AD-integratie met Google Apps, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a1a20-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="a1a20-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a1a20-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1a20-113">Een Google Apps eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a1a20-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1a20-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a1a20-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1a20-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a1a20-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1a20-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a1a20-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1a20-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1a20-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="a1a20-118">Zelfstudievideo</span><span class="sxs-lookup"><span data-stu-id="a1a20-118">Video tutorial</span></span>
<span data-ttu-id="a1a20-119">Het inschakelen van eenmalige aanmelding met Google Apps 2 minuten:</span><span class="sxs-lookup"><span data-stu-id="a1a20-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="a1a20-120">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="a1a20-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="a1a20-121">**V: Chromebooks en andere apparaten Chrome compatibel zijn met eenmalige aanmelding Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="a1a20-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="a1a20-122">A: Ja, kunnen gebruikers zich aanmelden bij hun Chromebook apparaten met hun Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="a1a20-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="a1a20-123">Zie dit [Google Apps ondersteunen artikel](https://support.google.com/chrome/a/answer/6060880) voor informatie over gebruikers mogelijk om wordt gevraagd referenties twee keer.</span><span class="sxs-lookup"><span data-stu-id="a1a20-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="a1a20-124">**V: als ik eenmalige aanmelding inschakelen, wordt gebruikers mogelijk hun Azure AD-referenties gebruiken om u te melden bij een Google-product, zoals Google leslokaal, GMail, Google Drive, YouTube, enzovoort?**</span><span class="sxs-lookup"><span data-stu-id="a1a20-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="a1a20-125">A: Ja, afhankelijk van [welke Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) u wilt in- of uitschakelen voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="a1a20-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="a1a20-126">**V: kan ik eenmalige aanmelding voor alleen een subset van mijn gebruikers Google Apps inschakelen?**</span><span class="sxs-lookup"><span data-stu-id="a1a20-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="a1a20-127">A: niet onmiddellijk bij eenmalige aanmelding inschakelen, moet uw Google Apps-gebruikers te verifiëren met hun Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="a1a20-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="a1a20-128">Omdat Google Apps biedt geen ondersteuning voor meerdere id-providers, de id-provider voor uw Google Apps-omgeving kan Azure AD zijn of Google-- maar niet beide op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="a1a20-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="a1a20-129">**V: als een gebruiker is aangemeld via Windows, worden dat ze automatisch een verificatie met Google Apps zonder gevraagd om een wachtwoord?**</span><span class="sxs-lookup"><span data-stu-id="a1a20-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="a1a20-130">A: Er zijn twee opties voor het inschakelen van dit scenario.</span><span class="sxs-lookup"><span data-stu-id="a1a20-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="a1a20-131">Eerst gebruikers kunnen aanmelden bij Windows 10-apparaten via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1a20-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="a1a20-132">U kunt ook gebruikers kunnen aanmelden bij Windows-apparaten die zijn lid van een domein in een lokale Active Directory die is ingeschakeld voor eenmalige aanmelding bij Azure AD via een [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) implementatie.</span><span class="sxs-lookup"><span data-stu-id="a1a20-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="a1a20-133">In beide gevallen moet u de stappen uitvoeren in de volgende zelfstudie voor eenmalige aanmelding tussen Azure AD inschakelen en Google Apps.</span><span class="sxs-lookup"><span data-stu-id="a1a20-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1a20-134">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a1a20-134">Scenario description</span></span>
<span data-ttu-id="a1a20-135">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a1a20-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1a20-136">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a1a20-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1a20-137">Google Apps uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a1a20-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="a1a20-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1a20-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="a1a20-139">Google Apps uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a1a20-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="a1a20-140">Voor het configureren van de integratie van Google Apps in Azure AD, moet u Google Apps uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a1a20-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1a20-141">**Als u wilt toevoegen Google Apps uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1a20-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1a20-142">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a1a20-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1a20-144">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a1a20-145">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-145">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a1a20-147">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1a20-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a1a20-149">Typ in het zoekvak **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-149">In the search box, type **Google Apps**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="a1a20-151">Selecteer in het deelvenster resultaten **Google Apps**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a1a20-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1a20-153">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1a20-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1a20-154">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Google Apps op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a1a20-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a1a20-155">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Google Apps in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="a1a20-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="a1a20-156">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Google Apps tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a1a20-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="a1a20-157">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="a1a20-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="a1a20-158">Om te configureren en testen van Azure AD eenmalige aanmelding met Google Apps, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a1a20-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1a20-159">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1a20-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a1a20-160">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1a20-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1a20-161">**[Maken van een testgebruiker Google Apps](#creating-a-google-apps-test-user)**  - Google Apps die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="a1a20-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1a20-162">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a1a20-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1a20-163">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a1a20-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1a20-164">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a1a20-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1a20-165">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Google Apps configureren.</span><span class="sxs-lookup"><span data-stu-id="a1a20-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="a1a20-166">**Voor het configureren van Azure AD eenmalige aanmelding met Google Apps, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1a20-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="a1a20-167">In de Azure-portal op de **Google Apps** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a1a20-169">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a1a20-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="a1a20-171">Op de **Google Apps Domain en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a1a20-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="a1a20-173">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="a1a20-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1a20-174">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="a1a20-174">This value is not real.</span></span> <span data-ttu-id="a1a20-175">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a1a20-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="a1a20-176">Neem contact op met de [Google ondersteuningsteam](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="a1a20-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="a1a20-177">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a1a20-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="a1a20-179">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a1a20-179">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a1a20-181">Op de **Google Apps-configuratie** sectie, klikt u op **Google Apps configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a1a20-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a1a20-182">Kopieer de **Sign-Out-URL, SAML Single Sign-On Service-URL en wijzigen wachtwoord URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a1a20-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="a1a20-184">Een nieuw tabblad openen in uw browser en meld u aan bij de [Google Apps-beheerconsole](http://admin.google.com/) met uw administrator-account.</span><span class="sxs-lookup"><span data-stu-id="a1a20-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="a1a20-185">Klik op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-185">Click **Security**.</span></span> <span data-ttu-id="a1a20-186">Als u de koppeling niet ziet, kan het verborgen onder de **meer besturingselementen** menu aan de onderkant van het scherm.</span><span class="sxs-lookup"><span data-stu-id="a1a20-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Klik op 'Security' (Beveiliging).][10]

9. <span data-ttu-id="a1a20-188">Op de **beveiliging** pagina, klikt u op **instellen van eenmalige aanmelding (SSO).**</span><span class="sxs-lookup"><span data-stu-id="a1a20-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Klik op eenmalige aanmelding.][11]

10. <span data-ttu-id="a1a20-190">Voer de volgende configuratiewijzigingen:</span><span class="sxs-lookup"><span data-stu-id="a1a20-190">Perform the following configuration changes:</span></span>
   
    ![Eenmalige aanmelding configureren][12]
   
    <span data-ttu-id="a1a20-192">a.</span><span class="sxs-lookup"><span data-stu-id="a1a20-192">a.</span></span> <span data-ttu-id="a1a20-193">Selecteer **Setup-SSO met derden identiteitsprovider**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="a1a20-194">b.</span><span class="sxs-lookup"><span data-stu-id="a1a20-194">b.</span></span> <span data-ttu-id="a1a20-195">In de **aanmelden pagina-URL** veld in Google Apps, plak de waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a1a20-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a1a20-196">c.</span><span class="sxs-lookup"><span data-stu-id="a1a20-196">c.</span></span> <span data-ttu-id="a1a20-197">In de **afmelden pagina-URL** veld in Google Apps, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a1a20-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="a1a20-198">d.</span><span class="sxs-lookup"><span data-stu-id="a1a20-198">d.</span></span> <span data-ttu-id="a1a20-199">In de **URL voor wachtwoord wijzigen** veld in Google Apps, plak de waarde van **wijzigen wachtwoord URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a1a20-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="a1a20-200">e.</span><span class="sxs-lookup"><span data-stu-id="a1a20-200">e.</span></span> <span data-ttu-id="a1a20-201">In Google Apps voor de **verificatiecertificaat**, upload het certificaat dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a1a20-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="a1a20-202">f.</span><span class="sxs-lookup"><span data-stu-id="a1a20-202">f.</span></span> <span data-ttu-id="a1a20-203">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a1a20-204">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a1a20-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a1a20-205">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a1a20-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a1a20-206">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1a20-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1a20-207">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a1a20-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1a20-208">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a1a20-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a1a20-210">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1a20-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1a20-211">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a1a20-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1a20-213">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1a20-215">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1a20-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1a20-217">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a1a20-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1a20-219">a.</span><span class="sxs-lookup"><span data-stu-id="a1a20-219">a.</span></span> <span data-ttu-id="a1a20-220">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1a20-221">b.</span><span class="sxs-lookup"><span data-stu-id="a1a20-221">b.</span></span> <span data-ttu-id="a1a20-222">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a1a20-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1a20-223">c.</span><span class="sxs-lookup"><span data-stu-id="a1a20-223">c.</span></span> <span data-ttu-id="a1a20-224">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a1a20-225">d.</span><span class="sxs-lookup"><span data-stu-id="a1a20-225">d.</span></span> <span data-ttu-id="a1a20-226">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="a1a20-227">Een testgebruiker Google Apps maken</span><span class="sxs-lookup"><span data-stu-id="a1a20-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="a1a20-228">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Google Apps Software.</span><span class="sxs-lookup"><span data-stu-id="a1a20-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="a1a20-229">Google Apps ondersteunt automatische inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a1a20-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="a1a20-230">Er is geen actie voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="a1a20-230">There is no action for you in this section.</span></span> <span data-ttu-id="a1a20-231">Als een gebruiker in Google Apps Software nog niet bestaat, wordt een nieuwe gemaakt wanneer u probeert te krijgen tot Software voor Google Apps.</span><span class="sxs-lookup"><span data-stu-id="a1a20-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="a1a20-232">Als u maken van een gebruiker handmatig wilt, neem dan contact op met de [Google ondersteuningsteam](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="a1a20-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a1a20-233">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1a20-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a1a20-234">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Google Apps.</span><span class="sxs-lookup"><span data-stu-id="a1a20-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a1a20-236">**Britta Simon om aan te wijzen Google Apps, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a1a20-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="a1a20-237">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a1a20-239">Selecteer in de lijst met toepassingen **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-239">In the applications list, select **Google Apps**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="a1a20-241">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a1a20-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a1a20-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a1a20-243">Click **Add** button.</span></span> <span data-ttu-id="a1a20-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1a20-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a1a20-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a1a20-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a1a20-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1a20-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1a20-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1a20-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1a20-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1a20-249">Testing single sign-on</span></span>

<span data-ttu-id="a1a20-250">In deze sectie voor het testen van uw instellingen voor eenmalige aanmelding, opent u het toegangsvenster op [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), meldt u zich bij de testaccount en klikt u op **Google Apps** tegel in het deelvenster toegang.</span><span class="sxs-lookup"><span data-stu-id="a1a20-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1a20-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a1a20-251">Additional resources</span></span>

* [<span data-ttu-id="a1a20-252">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1a20-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1a20-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1a20-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a1a20-254">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="a1a20-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png