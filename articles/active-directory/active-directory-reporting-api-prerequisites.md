---
title: aaaPrerequisites tooaccess hello Azure AD rapportage-API. | Microsoft Docs
description: Meer informatie over Hallo vereisten tooaccess hello Azure AD reporting API
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
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="07400-104">Vereisten tooaccess hello Azure AD rapportage-API</span><span class="sxs-lookup"><span data-stu-id="07400-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="07400-105">Hallo [Azure AD rapportage-API's](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) voorzien van toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="07400-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="07400-106">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="07400-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="07400-107">rapportage-API maakt gebruikt Hallo [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toegang toohello web-API's.</span><span class="sxs-lookup"><span data-stu-id="07400-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="07400-108">tooprepare uw toegang toohello rapportage-API, moet u:</span><span class="sxs-lookup"><span data-stu-id="07400-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="07400-109">Een toepassing in uw Azure AD-tenant maken</span><span class="sxs-lookup"><span data-stu-id="07400-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="07400-110">Verleen Hallo toepassing gemachtigd tooaccess hello Azure AD-gegevens</span><span class="sxs-lookup"><span data-stu-id="07400-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="07400-111">Verzamelen van configuratie-instellingen van uw directory</span><span class="sxs-lookup"><span data-stu-id="07400-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="07400-112">Voor vragen, problemen of feedback, neem contact op met [AAD rapportage Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="07400-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="07400-113">Een Azure AD-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="07400-113">Create an Azure AD application</span></span>
<span data-ttu-id="07400-114">tooconfigure uw directory tooaccess hello Azure AD reporting API, moet u zich aanmeldt toohello klassieke Azure-portal met een administrator-account voor Azure-abonnement is ook lid zijn van de rol van algemeen beheerder directory Hallo in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="07400-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07400-115">Toepassingen die worden uitgevoerd onder-referenties met bevoegdheden als volgt 'admin' kunnen zeer krachtig zijn, dus zorg ervoor dat tookeep Hallo van de toepassing-ID/geheim referenties veilig.</span><span class="sxs-lookup"><span data-stu-id="07400-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="07400-116">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07400-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="07400-118">Van Hallo **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="07400-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="07400-119">Klik in het menu bovenaan Hallo Hallo **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="07400-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="07400-121">Klik op de balk onderaan hello, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="07400-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="07400-123">Op Hallo **wat wilt u wilt dat toodo?** dialoogvenster, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="07400-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="07400-125">Op Hallo **Vertel ons over uw toepassing** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="07400-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="07400-127">a.</span><span class="sxs-lookup"><span data-stu-id="07400-127">a.</span></span> <span data-ttu-id="07400-128">In Hallo **naam** textbox, typ een naam (bijvoorbeeld: de toepassing van rapportage-API).</span><span class="sxs-lookup"><span data-stu-id="07400-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="07400-129">b.</span><span class="sxs-lookup"><span data-stu-id="07400-129">b.</span></span> <span data-ttu-id="07400-130">Selecteer **webtoepassing en/of web-API**.</span><span class="sxs-lookup"><span data-stu-id="07400-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="07400-131">c.</span><span class="sxs-lookup"><span data-stu-id="07400-131">c.</span></span> <span data-ttu-id="07400-132">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="07400-132">Click **Next**.</span></span>
7. <span data-ttu-id="07400-133">Op Hallo **App-eigenschappen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="07400-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="07400-135">a.</span><span class="sxs-lookup"><span data-stu-id="07400-135">a.</span></span> <span data-ttu-id="07400-136">In Hallo **aanmeldings-URL** textbox type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="07400-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="07400-137">b.</span><span class="sxs-lookup"><span data-stu-id="07400-137">b.</span></span> <span data-ttu-id="07400-138">In Hallo **App ID URI** textbox type ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="07400-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="07400-139">c.</span><span class="sxs-lookup"><span data-stu-id="07400-139">c.</span></span> <span data-ttu-id="07400-140">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="07400-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="07400-141">Uw toepassing machtiging toouse Hallo API verlenen</span><span class="sxs-lookup"><span data-stu-id="07400-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="07400-142">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07400-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="07400-144">Van Hallo **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="07400-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="07400-145">Klik in het menu bovenaan Hallo Hallo **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="07400-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="07400-147">Selecteer in de lijst met toepassingen van Hallo, uw nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="07400-147">In hello applications list, select your newly created application.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="07400-149">Klik in het menu bovenaan Hallo Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="07400-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="07400-151">In Hallo **machtigingen tooother toepassingen** sectie voor Hallo **Azure Active Directory** resource, klikt u op Hallo **Toepassingsmachtigingen** vervolgkeuzelijst, en vervolgens Selecteer **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="07400-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="07400-153">Klik op de balk onderaan hello, **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="07400-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="07400-155">Verzamelen van configuratie-instellingen van uw directory</span><span class="sxs-lookup"><span data-stu-id="07400-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="07400-156">Deze sectie leest u hoe tooget Hallo instellingen van uw directory te volgen:</span><span class="sxs-lookup"><span data-stu-id="07400-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="07400-157">Domeinnaam</span><span class="sxs-lookup"><span data-stu-id="07400-157">Domain name</span></span>
* <span data-ttu-id="07400-158">Client-ID</span><span class="sxs-lookup"><span data-stu-id="07400-158">Client ID</span></span>
* <span data-ttu-id="07400-159">Clientgeheim</span><span class="sxs-lookup"><span data-stu-id="07400-159">Client secret</span></span>

<span data-ttu-id="07400-160">U moet deze waarden bij het configureren van rapportage toohello-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="07400-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="07400-161">Uw domeinnaam ophalen</span><span class="sxs-lookup"><span data-stu-id="07400-161">Get your domain name</span></span>
1. <span data-ttu-id="07400-162">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07400-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="07400-164">Van Hallo **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="07400-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="07400-165">Klik in het menu bovenaan Hallo Hallo **domeinen**.</span><span class="sxs-lookup"><span data-stu-id="07400-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="07400-167">In Hallo **domeinnaam** kolom, kopieert u de domeinnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="07400-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="07400-169">Haal client-ID van de toepassing hello</span><span class="sxs-lookup"><span data-stu-id="07400-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="07400-170">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07400-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="07400-172">Van Hallo **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="07400-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="07400-173">Klik in het menu bovenaan Hallo Hallo **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="07400-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="07400-175">Selecteer in de lijst met toepassingen van Hallo, uw nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="07400-175">In hello applications list, select your newly created application.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="07400-177">Klik in het menu bovenaan Hallo Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="07400-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="07400-179">Kopieer uw **Client-ID**.</span><span class="sxs-lookup"><span data-stu-id="07400-179">Copy your **Client ID**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="07400-181">Van de toepassing hello clientgeheim ophalen</span><span class="sxs-lookup"><span data-stu-id="07400-181">Get hello application's client secret</span></span>
<span data-ttu-id="07400-182">tooget van uw toepassing client geheime, u moet een nieuwe sleutel toocreate en sla de waarde bij het opslaan van de nieuwe sleutel Hallo omdat het niet mogelijk tooretrieve deze waarde later niet meer.</span><span class="sxs-lookup"><span data-stu-id="07400-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="07400-183">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07400-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="07400-185">Van Hallo **active directory** Selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="07400-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="07400-186">Klik in het menu bovenaan Hallo Hallo **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="07400-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="07400-188">Selecteer in de lijst met toepassingen van Hallo, uw nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="07400-188">In hello applications list, select your newly created application.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="07400-190">Klik in het menu bovenaan Hallo Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="07400-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="07400-192">In Hallo **sleutels** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="07400-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="07400-194">a.</span><span class="sxs-lookup"><span data-stu-id="07400-194">a.</span></span> <span data-ttu-id="07400-195">Selecteer een duur in Hallo duur van de lijst.</span><span class="sxs-lookup"><span data-stu-id="07400-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="07400-196">b.</span><span class="sxs-lookup"><span data-stu-id="07400-196">b.</span></span> <span data-ttu-id="07400-197">Klik op de balk onderaan hello, **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="07400-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="07400-199">c.</span><span class="sxs-lookup"><span data-stu-id="07400-199">c.</span></span> <span data-ttu-id="07400-200">Hallo-sleutelwaarde kopiëren.</span><span class="sxs-lookup"><span data-stu-id="07400-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07400-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07400-201">Next Steps</span></span>
* <span data-ttu-id="07400-202">Zou u zoals tooaccess gegevens van Azure AD Hallo Hallo rapportage-API op een programmatische manier?</span><span class="sxs-lookup"><span data-stu-id="07400-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="07400-203">Bekijk [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="07400-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="07400-204">Als u toofind voor meer informatie over Azure Active Directory-rapportage wilt, Zie Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="07400-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

