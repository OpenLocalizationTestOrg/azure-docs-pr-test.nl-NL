---
title: Vereisten voor toegang tot de Azure AD rapportage-API. | Microsoft Docs
description: Meer informatie over de vereisten voor toegang tot de Azure AD rapportage-API
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="b5978-104">Vereisten voor toegang tot de Azure AD rapportage-API</span><span class="sxs-lookup"><span data-stu-id="b5978-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="b5978-105">De [Azure AD rapportage-API's](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) u programmatische toegang bieden tot de gegevens via een set op basis van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="b5978-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="b5978-106">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b5978-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="b5978-107">De rapportage-API maakt gebruikt [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) toegang verlenen aan de web-API's.</span><span class="sxs-lookup"><span data-stu-id="b5978-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="b5978-108">Als u met het voorbereiden van uw toegang tot de rapportage-API, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b5978-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="b5978-109">Een toepassing in uw Azure AD-tenant maken</span><span class="sxs-lookup"><span data-stu-id="b5978-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="b5978-110">Verleen de juiste toepassing worden machtigingen voor toegang tot de Azure AD-gegevens</span><span class="sxs-lookup"><span data-stu-id="b5978-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="b5978-111">Verzamelen van configuratie-instellingen van uw directory</span><span class="sxs-lookup"><span data-stu-id="b5978-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="b5978-112">Voor vragen, problemen of feedback, neem contact op met [AAD rapportage Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b5978-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="b5978-113">Een Azure AD-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="b5978-113">Create an Azure AD application</span></span>
<span data-ttu-id="b5978-114">Voor het configureren van uw directory voor toegang tot de Azure AD rapportage-API, moet u zich aanmeldt bij de klassieke Azure portal met een administrator-account voor Azure-abonnement is ook lid zijn van de rol globale beheerder directory in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="b5978-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5978-115">Toepassingen die worden uitgevoerd onder-referenties met bevoegdheden als volgt 'admin' kunnen zeer krachtig zijn, dus zorg ervoor dat de toepassing-ID/geheim referenties veilig te houden.</span><span class="sxs-lookup"><span data-stu-id="b5978-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="b5978-116">In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5978-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b5978-118">Van de **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="b5978-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b5978-119">Klik in het menu bovenaan op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="b5978-121">Klik op de balk onderaan **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-121">On the bottom bar, click **Add**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="b5978-123">Op de **wat wilt u doen?** dialoogvenster, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="b5978-125">Op de **Vertel ons over uw toepassing** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b5978-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="b5978-127">a.</span><span class="sxs-lookup"><span data-stu-id="b5978-127">a.</span></span> <span data-ttu-id="b5978-128">In de **naam** textbox, typ een naam (bijvoorbeeld: de toepassing van rapportage-API).</span><span class="sxs-lookup"><span data-stu-id="b5978-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="b5978-129">b.</span><span class="sxs-lookup"><span data-stu-id="b5978-129">b.</span></span> <span data-ttu-id="b5978-130">Selecteer **webtoepassing en/of web-API**.</span><span class="sxs-lookup"><span data-stu-id="b5978-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="b5978-131">c.</span><span class="sxs-lookup"><span data-stu-id="b5978-131">c.</span></span> <span data-ttu-id="b5978-132">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5978-132">Click **Next**.</span></span>
7. <span data-ttu-id="b5978-133">Op de **App-eigenschappen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b5978-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="b5978-135">a.</span><span class="sxs-lookup"><span data-stu-id="b5978-135">a.</span></span> <span data-ttu-id="b5978-136">In de **aanmeldings-URL** textbox type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="b5978-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="b5978-137">b.</span><span class="sxs-lookup"><span data-stu-id="b5978-137">b.</span></span> <span data-ttu-id="b5978-138">In de **App ID URI** textbox type ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="b5978-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="b5978-139">c.</span><span class="sxs-lookup"><span data-stu-id="b5978-139">c.</span></span> <span data-ttu-id="b5978-140">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b5978-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="b5978-141">Uw toepassing toestemming de API gebruiken</span><span class="sxs-lookup"><span data-stu-id="b5978-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="b5978-142">In de [klassieke Azure-portal](https://manage.windowsazure.com/), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5978-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b5978-144">Van de **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="b5978-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b5978-145">Klik in het menu bovenaan op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="b5978-147">Selecteer uw nieuwe toepassing in de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b5978-147">In the applications list, select your newly created application.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="b5978-149">Klik in het menu bovenaan op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="b5978-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="b5978-151">In de **machtigingen voor andere toepassingen** sectie voor de **Azure Active Directory** resource, klikt u op de **Toepassingsmachtigingen** vervolgkeuzelijst en selecteer vervolgens **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="b5978-153">Klik op de balk onderaan **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b5978-153">On the bottom bar, click **Save**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="b5978-155">Verzamelen van configuratie-instellingen van uw directory</span><span class="sxs-lookup"><span data-stu-id="b5978-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="b5978-156">Deze sectie wordt beschreven hoe u de volgende instellingen van uw directory ophalen:</span><span class="sxs-lookup"><span data-stu-id="b5978-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="b5978-157">Domeinnaam</span><span class="sxs-lookup"><span data-stu-id="b5978-157">Domain name</span></span>
* <span data-ttu-id="b5978-158">Client-ID</span><span class="sxs-lookup"><span data-stu-id="b5978-158">Client ID</span></span>
* <span data-ttu-id="b5978-159">Clientgeheim</span><span class="sxs-lookup"><span data-stu-id="b5978-159">Client secret</span></span>

<span data-ttu-id="b5978-160">U moet deze waarden bij het configureren van de rapportage-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b5978-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="b5978-161">Uw domeinnaam ophalen</span><span class="sxs-lookup"><span data-stu-id="b5978-161">Get your domain name</span></span>
1. <span data-ttu-id="b5978-162">In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5978-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b5978-164">Van de **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="b5978-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b5978-165">Klik in het menu bovenaan op **domeinen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="b5978-167">In de **domeinnaam** kolom, kopieert u de domeinnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="b5978-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="b5978-169">Client-ID van de toepassing ophalen</span><span class="sxs-lookup"><span data-stu-id="b5978-169">Get the application's client ID</span></span>
1. <span data-ttu-id="b5978-170">In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5978-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b5978-172">Van de **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="b5978-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b5978-173">Klik in het menu bovenaan op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="b5978-175">Selecteer uw nieuwe toepassing in de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b5978-175">In the applications list, select your newly created application.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="b5978-177">Klik in het menu bovenaan op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="b5978-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="b5978-179">Kopieer uw **Client-ID**.</span><span class="sxs-lookup"><span data-stu-id="b5978-179">Copy your **Client ID**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="b5978-181">Clientgeheim van de toepassing ophalen</span><span class="sxs-lookup"><span data-stu-id="b5978-181">Get the application's client secret</span></span>
<span data-ttu-id="b5978-182">Als u uw toepassing clientgeheim, moet u een nieuwe sleutel maken en opslaan van de waarde bij het opslaan van de nieuwe sleutel, omdat het is niet mogelijk is deze waarde later meer ophalen.</span><span class="sxs-lookup"><span data-stu-id="b5978-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="b5978-183">In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5978-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="b5978-185">Van de **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="b5978-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="b5978-186">Klik in het menu bovenaan op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5978-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="b5978-188">Selecteer uw nieuwe toepassing in de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b5978-188">In the applications list, select your newly created application.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="b5978-190">Klik in het menu bovenaan op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="b5978-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="b5978-192">In de **sleutels** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5978-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="b5978-194">a.</span><span class="sxs-lookup"><span data-stu-id="b5978-194">a.</span></span> <span data-ttu-id="b5978-195">In de duur van de lijst, selecteert u een duur</span><span class="sxs-lookup"><span data-stu-id="b5978-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="b5978-196">b.</span><span class="sxs-lookup"><span data-stu-id="b5978-196">b.</span></span> <span data-ttu-id="b5978-197">Klik op de balk onderaan **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b5978-197">On the bottom bar, click **Save**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="b5978-199">c.</span><span class="sxs-lookup"><span data-stu-id="b5978-199">c.</span></span> <span data-ttu-id="b5978-200">Kopieer de waarde van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="b5978-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5978-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5978-201">Next Steps</span></span>
* <span data-ttu-id="b5978-202">Wilt u de toegang tot de gegevens van de Azure AD rapportage-API op een programmatische manier?</span><span class="sxs-lookup"><span data-stu-id="b5978-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="b5978-203">Bekijk [aan de slag met Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b5978-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="b5978-204">Als u meer informatie over Azure Active Directory-rapportage wilt, raadpleegt u de [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b5978-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

