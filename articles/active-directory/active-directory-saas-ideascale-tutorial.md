---
title: 'Zelfstudie: Azure Active Directory-integratie met IdeaScale | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en IdeaScale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="2ab4a-103">Zelfstudie: Azure Active Directory-integratie met IdeaScale</span><span class="sxs-lookup"><span data-stu-id="2ab4a-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="2ab4a-104">In deze zelfstudie leert u hoe IdeaScale integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ab4a-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ab4a-105">IdeaScale integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2ab4a-106">U kunt beheren in Azure AD die toegang tot IdeaScale heeft</span><span class="sxs-lookup"><span data-stu-id="2ab4a-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="2ab4a-107">U kunt uw gebruikers automatisch ophalen aangemeld bij IdeaScale (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2ab4a-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ab4a-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2ab4a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2ab4a-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ab4a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ab4a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2ab4a-110">Prerequisites</span></span>

<span data-ttu-id="2ab4a-111">Voor het configureren van Azure AD-integratie met IdeaScale, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="2ab4a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2ab4a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ab4a-113">Een IdeaScale eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2ab4a-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ab4a-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ab4a-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ab4a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ab4a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ab4a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ab4a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2ab4a-118">Scenario description</span></span>
<span data-ttu-id="2ab4a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ab4a-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ab4a-121">IdeaScale uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2ab4a-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="2ab4a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2ab4a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="2ab4a-123">IdeaScale uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2ab4a-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="2ab4a-124">Voor het configureren van de integratie van IdeaScale in Azure AD, moet u IdeaScale uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2ab4a-125">**Als u wilt toevoegen IdeaScale uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2ab4a-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2ab4a-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ab4a-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2ab4a-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2ab4a-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2ab4a-133">Typ in het zoekvak **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-133">In the search box, type **IdeaScale**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="2ab4a-135">Selecteer in het deelvenster resultaten **IdeaScale**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ab4a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2ab4a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ab4a-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met IdeaScale op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2ab4a-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2ab4a-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in IdeaScale is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="2ab4a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in IdeaScale tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="2ab4a-141">Wijs in IdeaScale, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2ab4a-142">Om te configureren en testen van Azure AD eenmalige aanmelding met IdeaScale, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2ab4a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2ab4a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ab4a-145">**[Maken van een testgebruiker IdeaScale](#creating-an-ideascale-test-user)**  - IdeaScale die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ab4a-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ab4a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ab4a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2ab4a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ab4a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing IdeaScale configureren.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="2ab4a-150">**Voor het configureren van Azure AD eenmalige aanmelding met IdeaScale, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2ab4a-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="2ab4a-151">In de Azure-portal op de **IdeaScale** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2ab4a-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="2ab4a-155">Op de **IdeaScale domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="2ab4a-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-157">a.</span></span> <span data-ttu-id="2ab4a-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="2ab4a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="2ab4a-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-159">b.</span></span> <span data-ttu-id="2ab4a-160">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="2ab4a-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-161">These values are not real.</span></span> <span data-ttu-id="2ab4a-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2ab4a-163">Neem contact op met [IdeaScale Client ondersteuningsteam](http://support.ideascale.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="2ab4a-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="2ab4a-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ab4a-168">Op de **IdeaScale configuratie** sectie, klikt u op **configureren IdeaScale** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2ab4a-169">Kopieer de **Sign-Out-URL en SAML entiteit-ID** van de **Naslaggids punt**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="2ab4a-171">In een ander browservenster, meld u aan bij uw bedrijf IdeaScale site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="2ab4a-172">Ga naar **Community instellingen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="2ab4a-173">![Instellingen van de community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community-instellingen")</span><span class="sxs-lookup"><span data-stu-id="2ab4a-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="2ab4a-174">Ga naar **beveiliging \> eenmalige aanmelding instellingen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="2ab4a-175">![Eenmalige aanmelding instellingen](./media/active-directory-saas-ideascale-tutorial/ic790848.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="2ab4a-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="2ab4a-176">Als **eenmaal aanmelden Type**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="2ab4a-177">![Eenmalige aanmelding Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "eenmalige aanmelding Type")</span><span class="sxs-lookup"><span data-stu-id="2ab4a-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="2ab4a-178">Op de **instellingen voor eenmalige aanmelding** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="2ab4a-179">![Eenmalige aanmelding instellingen](./media/active-directory-saas-ideascale-tutorial/ic790850.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="2ab4a-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="2ab4a-180">a.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-180">a.</span></span> <span data-ttu-id="2ab4a-181">In **SAML IdP entiteit-ID** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ab4a-182">b.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-182">b.</span></span> <span data-ttu-id="2ab4a-183">De inhoud van uw van het gedownloade metagegevensbestand kopiëren vanuit Azure-portal en plak deze in de **SAML IdP metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="2ab4a-184">c.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-184">c.</span></span> <span data-ttu-id="2ab4a-185">In **afmelding geslaagd URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ab4a-186">d.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-186">d.</span></span> <span data-ttu-id="2ab4a-187">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2ab4a-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="2ab4a-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2ab4a-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2ab4a-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ab4a-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ab4a-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2ab4a-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ab4a-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2ab4a-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2ab4a-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2ab4a-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ab4a-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ab4a-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ab4a-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ab4a-203">a.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-203">a.</span></span> <span data-ttu-id="2ab4a-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ab4a-205">b.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-205">b.</span></span> <span data-ttu-id="2ab4a-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ab4a-207">c.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-207">c.</span></span> <span data-ttu-id="2ab4a-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2ab4a-209">d.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-209">d.</span></span> <span data-ttu-id="2ab4a-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="2ab4a-211">Een testgebruiker IdeaScale maken</span><span class="sxs-lookup"><span data-stu-id="2ab4a-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="2ab4a-212">Om Azure AD-gebruikers aan te melden bij IdeaScale, moeten ze worden ingericht op IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="2ab4a-213">In het geval van IdeaScale is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="2ab4a-214">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2ab4a-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="2ab4a-215">Meld u aan bij uw **IdeaScale** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="2ab4a-216">Ga naar **Community instellingen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="2ab4a-217">![Instellingen van de community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community-instellingen")</span><span class="sxs-lookup"><span data-stu-id="2ab4a-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="2ab4a-218">Ga naar **basisinstellingen \> lid Management**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="2ab4a-219">Klik op **lid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="2ab4a-220">![Lid Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "lid Management")</span><span class="sxs-lookup"><span data-stu-id="2ab4a-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="2ab4a-221">Voer de volgende stappen uit in de sectie Nieuw lid toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2ab4a-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="2ab4a-222">![Nieuw lid toevoegt](./media/active-directory-saas-ideascale-tutorial/ic790853.png "nieuw lid toevoegt")</span><span class="sxs-lookup"><span data-stu-id="2ab4a-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="2ab4a-223">a.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-223">a.</span></span> <span data-ttu-id="2ab4a-224">In de **e-mailadressen** textbox, typ de e-mailadres van een geldige AAD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="2ab4a-225">b.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-225">b.</span></span> <span data-ttu-id="2ab4a-226">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="2ab4a-227">De Azure Active Directory-accounthouder Hiermee haalt u een e-mailbericht met een koppeling naar het account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="2ab4a-228">U kunt andere IdeaScale gebruiker account hulpmiddelen voor het maken of API's die is geleverd door IdeaScale aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2ab4a-229">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ab4a-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2ab4a-230">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2ab4a-232">**Britta Simon om aan te wijzen IdeaScale, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2ab4a-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="2ab4a-233">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2ab4a-235">Selecteer in de lijst met toepassingen **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-235">In the applications list, select **IdeaScale**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="2ab4a-237">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2ab4a-239">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-239">Click **Add** button.</span></span> <span data-ttu-id="2ab4a-240">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2ab4a-242">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2ab4a-243">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ab4a-244">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ab4a-245">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2ab4a-245">Testing single sign-on</span></span>


<span data-ttu-id="2ab4a-246">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2ab4a-247">Als u op de tegel IdeaScale in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="2ab4a-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ab4a-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2ab4a-248">Additional resources</span></span>

* [<span data-ttu-id="2ab4a-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ab4a-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ab4a-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ab4a-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

