---
title: aaaPrerequisites tooaccess hello Azure AD reporting API | Microsoft Docs
description: Meer informatie over Hallo vereisten tooaccess hello Azure AD reporting API
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="984c6-103">Vereisten tooaccess hello Azure AD rapportage-API</span><span class="sxs-lookup"><span data-stu-id="984c6-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="984c6-104">Hallo [Azure AD rapportage-API's](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) voorzien van toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="984c6-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="984c6-105">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="984c6-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="984c6-106">rapportage-API maakt gebruikt Hallo [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toegang toohello web-API's.</span><span class="sxs-lookup"><span data-stu-id="984c6-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="984c6-107">tooget toohello reporting gegevens benaderen via Hallo API, moet u toohave een van de volgende rollen toegewezen Hallo:</span><span class="sxs-lookup"><span data-stu-id="984c6-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="984c6-108">Beveiliging lezer</span><span class="sxs-lookup"><span data-stu-id="984c6-108">Security Reader</span></span>
- <span data-ttu-id="984c6-109">De beheerder beveiliging</span><span class="sxs-lookup"><span data-stu-id="984c6-109">Security Admin</span></span>
- <span data-ttu-id="984c6-110">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="984c6-110">Global Admin</span></span>


<span data-ttu-id="984c6-111">tooprepare uw toegang toohello rapportage-API, moet u:</span><span class="sxs-lookup"><span data-stu-id="984c6-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="984c6-112">Een toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="984c6-112">Register an application</span></span> 
2. <span data-ttu-id="984c6-113">Machtigingen toekennen</span><span class="sxs-lookup"><span data-stu-id="984c6-113">Grant permissions</span></span> 
3. <span data-ttu-id="984c6-114">Verzamelen van configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="984c6-114">Gather configuration settings</span></span> 

<span data-ttu-id="984c6-115">Voor vragen, problemen of feedback, neemt u [een ondersteuningsticket bestand](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="984c6-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="984c6-116">Een Azure Active Directory-toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="984c6-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="984c6-117">U moet tooregister een app, zelfs als u Hallo rapportage-API met een script opent.</span><span class="sxs-lookup"><span data-stu-id="984c6-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="984c6-118">Hiermee krijgt u een **toepassings-ID**, die is vereist voor een aanroep van de autorisatie en kunnen uw code tooreceive-tokens.</span><span class="sxs-lookup"><span data-stu-id="984c6-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="984c6-119">tooconfigure uw directory tooaccess hello Azure AD reporting API, moet u zich aanmeldt toohello Azure-portal met een Azure-beheerdersaccount die ook lid zijn van Hallo **hoofdbeheerder** directory-rol in uw Azure AD-tenant .</span><span class="sxs-lookup"><span data-stu-id="984c6-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="984c6-120">Toepassingen die worden uitgevoerd onder-referenties met bevoegdheden als volgt 'admin' kunnen zeer krachtig zijn, dus zorg ervoor dat tookeep Hallo van de toepassing-ID/geheim referenties veilig.</span><span class="sxs-lookup"><span data-stu-id="984c6-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="984c6-121">**tooregister een Azure Active Directory-toepassing:**</span><span class="sxs-lookup"><span data-stu-id="984c6-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="984c6-122">In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="984c6-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="984c6-124">Op Hallo **Azure Active Directory** blade, klikt u op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="984c6-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="984c6-126">Op Hallo **App registraties** blade in de werkbalk Hallo op Hallo boven, klikt u op **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="984c6-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="984c6-128">Op Hallo **maken** blade Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="984c6-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="984c6-130">a.</span><span class="sxs-lookup"><span data-stu-id="984c6-130">a.</span></span> <span data-ttu-id="984c6-131">In Hallo **naam** textbox type `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="984c6-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="984c6-132">b.</span><span class="sxs-lookup"><span data-stu-id="984c6-132">b.</span></span> <span data-ttu-id="984c6-133">Als **toepassingstype**, selecteer **Web-app / API**.</span><span class="sxs-lookup"><span data-stu-id="984c6-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="984c6-134">c.</span><span class="sxs-lookup"><span data-stu-id="984c6-134">c.</span></span> <span data-ttu-id="984c6-135">In Hallo **aanmeldings-URL** textbox type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="984c6-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="984c6-136">d.</span><span class="sxs-lookup"><span data-stu-id="984c6-136">d.</span></span> <span data-ttu-id="984c6-137">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="984c6-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="984c6-138">Machtigingen toekennen</span><span class="sxs-lookup"><span data-stu-id="984c6-138">Grant permissions</span></span> 

<span data-ttu-id="984c6-139">Hallo-doel van deze stap is toogrant uw toepassing **mapgegevens lezen** machtigingen toohello **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="984c6-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="984c6-141">**toogrant uw toepassing machtiging toouse Hallo API:**</span><span class="sxs-lookup"><span data-stu-id="984c6-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="984c6-142">Op Hallo **App registraties** blade in de lijst met apps van hello, klikt u op **rapportage-API-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="984c6-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="984c6-143">Op Hallo **rapportage-API-toepassing** blade in de werkbalk Hallo op Hallo boven, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="984c6-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="984c6-145">Op Hallo **instellingen** blade, klikt u op **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="984c6-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="984c6-147">Op Hallo **vereist machtigingen** blade in Hallo **API** lijst, klikt u op **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="984c6-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="984c6-149">Op Hallo **toegang inschakelen** blade Selecteer **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="984c6-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="984c6-151">Klik in de werkbalk bovenaan Hallo Hallo op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="984c6-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="984c6-153">Verzamelen van configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="984c6-153">Gather configuration settings</span></span> 
<span data-ttu-id="984c6-154">Deze sectie leest u hoe tooget Hallo instellingen van uw directory te volgen:</span><span class="sxs-lookup"><span data-stu-id="984c6-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="984c6-155">Domeinnaam</span><span class="sxs-lookup"><span data-stu-id="984c6-155">Domain name</span></span>
* <span data-ttu-id="984c6-156">Client-ID</span><span class="sxs-lookup"><span data-stu-id="984c6-156">Client ID</span></span>
* <span data-ttu-id="984c6-157">Clientgeheim</span><span class="sxs-lookup"><span data-stu-id="984c6-157">Client secret</span></span>

<span data-ttu-id="984c6-158">U moet deze waarden bij het configureren van rapportage toohello-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="984c6-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="984c6-159">Uw domeinnaam ophalen</span><span class="sxs-lookup"><span data-stu-id="984c6-159">Get your domain name</span></span>

<span data-ttu-id="984c6-160">**tooget uw domeinnaam:**</span><span class="sxs-lookup"><span data-stu-id="984c6-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="984c6-161">In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="984c6-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="984c6-163">Op Hallo **Azure Active Directory** blade, klikt u op **domeinnamen**.</span><span class="sxs-lookup"><span data-stu-id="984c6-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="984c6-165">Uw domeinnaam van de lijst met domeinen Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="984c6-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="984c6-166">Haal client-ID van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="984c6-166">Get your application's client ID</span></span>

<span data-ttu-id="984c6-167">**tooget van uw toepassing de client-ID:**</span><span class="sxs-lookup"><span data-stu-id="984c6-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="984c6-168">In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="984c6-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="984c6-170">Op Hallo **App registraties** blade in de lijst met apps van hello, klikt u op **rapportage-API-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="984c6-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="984c6-171">Op Hallo **rapportage-API-toepassing** blade op Hallo **toepassings-ID**, klikt u op **klikt u op toocopy**.</span><span class="sxs-lookup"><span data-stu-id="984c6-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="984c6-173">Uw toepassing clientgeheim ophalen</span><span class="sxs-lookup"><span data-stu-id="984c6-173">Get your application's client secret</span></span>
<span data-ttu-id="984c6-174">tooget van uw toepassing client geheime, u moet een nieuwe sleutel toocreate en sla de waarde bij het opslaan van de nieuwe sleutel Hallo omdat het niet mogelijk tooretrieve deze waarde later niet meer.</span><span class="sxs-lookup"><span data-stu-id="984c6-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="984c6-175">**tooget clientgeheim van uw toepassing:**</span><span class="sxs-lookup"><span data-stu-id="984c6-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="984c6-176">In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="984c6-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="984c6-178">Op Hallo **App registraties** blade in de lijst met apps van hello, klikt u op **rapportage-API-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="984c6-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="984c6-179">Op Hallo **rapportage-API-toepassing** blade in de werkbalk Hallo op Hallo boven, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="984c6-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="984c6-181">Op Hallo **instellingen** blade in Hallo **APIR toegang** sectie, klikt u op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="984c6-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="984c6-183">Op Hallo **sleutels** blade Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="984c6-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="984c6-185">a.</span><span class="sxs-lookup"><span data-stu-id="984c6-185">a.</span></span> <span data-ttu-id="984c6-186">In Hallo **beschrijving** textbox type `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="984c6-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="984c6-187">b.</span><span class="sxs-lookup"><span data-stu-id="984c6-187">b.</span></span> <span data-ttu-id="984c6-188">Als **verloopt**, selecteer **In 2 jaar**.</span><span class="sxs-lookup"><span data-stu-id="984c6-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="984c6-189">c.</span><span class="sxs-lookup"><span data-stu-id="984c6-189">c.</span></span> <span data-ttu-id="984c6-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="984c6-190">Click **Save**.</span></span>

    <span data-ttu-id="984c6-191">d.</span><span class="sxs-lookup"><span data-stu-id="984c6-191">d.</span></span> <span data-ttu-id="984c6-192">Hallo-sleutelwaarde kopiëren.</span><span class="sxs-lookup"><span data-stu-id="984c6-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="984c6-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="984c6-193">Next Steps</span></span>
* <span data-ttu-id="984c6-194">Zou u zoals tooaccess gegevens van Azure AD Hallo Hallo rapportage-API op een programmatische manier?</span><span class="sxs-lookup"><span data-stu-id="984c6-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="984c6-195">Bekijk [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="984c6-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="984c6-196">Als u toofind voor meer informatie over Azure Active Directory-rapportage wilt, Zie Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="984c6-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

