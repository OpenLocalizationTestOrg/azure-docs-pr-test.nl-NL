---
title: Vereisten voor toegang tot de Azure AD rapportage-API | Microsoft Docs
description: Meer informatie over de vereisten voor toegang tot de Azure AD rapportage-API
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
ms.openlocfilehash: 5fafd83c337e3c73260d89cdad7409a01ce5855b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="51fb7-103">Vereisten voor toegang tot de Azure AD rapportage-API</span><span class="sxs-lookup"><span data-stu-id="51fb7-103">Prerequisites to access the Azure AD reporting API</span></span>

<span data-ttu-id="51fb7-104">De [Azure AD rapportage-API's](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) u programmatische toegang bieden tot de gegevens via een set op basis van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="51fb7-104">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="51fb7-105">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="51fb7-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="51fb7-106">De rapportage-API maakt gebruikt [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) toegang verlenen aan de web-API's.</span><span class="sxs-lookup"><span data-stu-id="51fb7-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="51fb7-107">Als u toegang tot de rapportagegegevens via de API, moet u een van de volgende rollen toegewezen:</span><span class="sxs-lookup"><span data-stu-id="51fb7-107">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="51fb7-108">Beveiliging lezer</span><span class="sxs-lookup"><span data-stu-id="51fb7-108">Security Reader</span></span>
- <span data-ttu-id="51fb7-109">De beheerder beveiliging</span><span class="sxs-lookup"><span data-stu-id="51fb7-109">Security Admin</span></span>
- <span data-ttu-id="51fb7-110">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="51fb7-110">Global Admin</span></span>


<span data-ttu-id="51fb7-111">Als u met het voorbereiden van uw toegang tot de rapportage-API, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="51fb7-111">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="51fb7-112">Een toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="51fb7-112">Register an application</span></span> 
2. <span data-ttu-id="51fb7-113">Machtigingen toekennen</span><span class="sxs-lookup"><span data-stu-id="51fb7-113">Grant permissions</span></span> 
3. <span data-ttu-id="51fb7-114">Verzamelen van configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="51fb7-114">Gather configuration settings</span></span> 

<span data-ttu-id="51fb7-115">Voor vragen, problemen of feedback, neemt u [een ondersteuningsticket bestand](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="51fb7-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="51fb7-116">Een Azure Active Directory-toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="51fb7-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="51fb7-117">U moet een app registreren, zelfs als u de rapportage-API met een script opent.</span><span class="sxs-lookup"><span data-stu-id="51fb7-117">You need to register an app even if you are accessing the reporting API using a script.</span></span> <span data-ttu-id="51fb7-118">Hiermee krijgt u een **toepassings-ID**, die is vereist voor een aanroep van de autorisatie en kunnen uw code te ontvangen van tokens.</span><span class="sxs-lookup"><span data-stu-id="51fb7-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="51fb7-119">Voor het configureren van uw directory voor toegang tot de Azure AD rapportage-API, moet u zich aanmelden bij de Azure-portal met een Azure-beheerdersaccount die ook lid zijn van de **hoofdbeheerder** directory-rol in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="51fb7-119">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51fb7-120">Toepassingen die worden uitgevoerd onder-referenties met bevoegdheden als volgt 'admin' kunnen zeer krachtig zijn, dus zorg ervoor dat de toepassing-ID/geheim referenties veilig te houden.</span><span class="sxs-lookup"><span data-stu-id="51fb7-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="51fb7-121">**Een Azure Active Directory-toepassing registreren:**</span><span class="sxs-lookup"><span data-stu-id="51fb7-121">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="51fb7-122">In de [Azure-portal](https://portal.azure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-122">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="51fb7-124">Op de **Azure Active Directory** blade, klikt u op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-124">On the **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="51fb7-126">Op de **App registraties** blade in de werkbalk bovenaan, klikt u op **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-126">On the **App registrations** blade, in the toolbar on the top, click **New application registration**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="51fb7-128">Op de **maken** blade, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="51fb7-128">On the **Create** blade, perform the following steps:</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="51fb7-130">a.</span><span class="sxs-lookup"><span data-stu-id="51fb7-130">a.</span></span> <span data-ttu-id="51fb7-131">In de **naam** textbox type `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="51fb7-131">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="51fb7-132">b.</span><span class="sxs-lookup"><span data-stu-id="51fb7-132">b.</span></span> <span data-ttu-id="51fb7-133">Als **toepassingstype**, selecteer **Web-app / API**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="51fb7-134">c.</span><span class="sxs-lookup"><span data-stu-id="51fb7-134">c.</span></span> <span data-ttu-id="51fb7-135">In de **aanmeldings-URL** textbox type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="51fb7-135">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="51fb7-136">d.</span><span class="sxs-lookup"><span data-stu-id="51fb7-136">d.</span></span> <span data-ttu-id="51fb7-137">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="51fb7-138">Machtigingen toekennen</span><span class="sxs-lookup"><span data-stu-id="51fb7-138">Grant permissions</span></span> 

<span data-ttu-id="51fb7-139">Het doel van deze stap is het verlenen van uw toepassing **mapgegevens lezen** machtigingen voor de **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="51fb7-139">The objective of this step is to grant your application **Read directory data** permissions to the **Windows Azure Active Directory** API.</span></span>

![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="51fb7-141">**Uw toepassing om machtiging te verlenen aan de API gebruiken:**</span><span class="sxs-lookup"><span data-stu-id="51fb7-141">**To grant your application permission to use the API:**</span></span>

1. <span data-ttu-id="51fb7-142">Op de **App registraties** blade in de lijst met apps, klikt u op **rapportage-API-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-142">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="51fb7-143">Op de **rapportage-API-toepassing** blade in de werkbalk bovenaan, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-143">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="51fb7-145">Op de **instellingen** blade, klikt u op **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-145">On the **Settings** blade, click **Required permissions**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="51fb7-147">Op de **vereist machtigingen** blade in de **API** lijst, klikt u op **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-147">On the **Required permissions** blade, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="51fb7-149">Op de **toegang inschakelen** blade Selecteer **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-149">On the **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="51fb7-151">Klik in de werkbalk bovenaan op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-151">In the toolbar on the top, click **Save**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="51fb7-153">Verzamelen van configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="51fb7-153">Gather configuration settings</span></span> 
<span data-ttu-id="51fb7-154">Deze sectie wordt beschreven hoe u de volgende instellingen van uw directory ophalen:</span><span class="sxs-lookup"><span data-stu-id="51fb7-154">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="51fb7-155">Domeinnaam</span><span class="sxs-lookup"><span data-stu-id="51fb7-155">Domain name</span></span>
* <span data-ttu-id="51fb7-156">Client-ID</span><span class="sxs-lookup"><span data-stu-id="51fb7-156">Client ID</span></span>
* <span data-ttu-id="51fb7-157">Clientgeheim</span><span class="sxs-lookup"><span data-stu-id="51fb7-157">Client secret</span></span>

<span data-ttu-id="51fb7-158">U moet deze waarden bij het configureren van de rapportage-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="51fb7-158">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="51fb7-159">Uw domeinnaam ophalen</span><span class="sxs-lookup"><span data-stu-id="51fb7-159">Get your domain name</span></span>

<span data-ttu-id="51fb7-160">**Uw domeinnaam ophalen:**</span><span class="sxs-lookup"><span data-stu-id="51fb7-160">**To get your domain name:**</span></span>

1. <span data-ttu-id="51fb7-161">In de [Azure-portal](https://portal.azure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-161">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="51fb7-163">Op de **Azure Active Directory** blade, klikt u op **domeinnamen**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-163">On the **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="51fb7-165">Kopieer uw domeinnaam van de lijst met domeinen.</span><span class="sxs-lookup"><span data-stu-id="51fb7-165">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="51fb7-166">Haal client-ID van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="51fb7-166">Get your application's client ID</span></span>

<span data-ttu-id="51fb7-167">**Ophalen van uw toepassing de client-ID:**</span><span class="sxs-lookup"><span data-stu-id="51fb7-167">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="51fb7-168">In de [Azure-portal](https://portal.azure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-168">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="51fb7-170">Op de **App registraties** blade in de lijst met apps, klikt u op **rapportage-API-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-170">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="51fb7-171">Op de **rapportage-API-toepassing** blade op de **toepassings-ID**, klikt u op **Klik hier om te kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-171">On the **Reporting API application** blade, at the **Application ID**, click **Click to copy**.</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="51fb7-173">Uw toepassing clientgeheim ophalen</span><span class="sxs-lookup"><span data-stu-id="51fb7-173">Get your application's client secret</span></span>
<span data-ttu-id="51fb7-174">Als u uw toepassing clientgeheim, moet u een nieuwe sleutel maken en opslaan van de waarde bij het opslaan van de nieuwe sleutel, omdat het is niet mogelijk is deze waarde later meer ophalen.</span><span class="sxs-lookup"><span data-stu-id="51fb7-174">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="51fb7-175">**Ophalen van uw toepassing clientgeheim:**</span><span class="sxs-lookup"><span data-stu-id="51fb7-175">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="51fb7-176">In de [Azure-portal](https://portal.azure.com), klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-176">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="51fb7-178">Op de **App registraties** blade in de lijst met apps, klikt u op **rapportage-API-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-178">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="51fb7-179">Op de **rapportage-API-toepassing** blade in de werkbalk bovenaan, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-179">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="51fb7-181">Op de **instellingen** blade in de **APIR toegang** sectie, klikt u op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-181">On the **Settings** blade, in the **APIR Access** section, click **Keys**.</span></span> 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="51fb7-183">Op de **sleutels** blade, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="51fb7-183">On the **Keys** blade, perform the following steps:</span></span>

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="51fb7-185">a.</span><span class="sxs-lookup"><span data-stu-id="51fb7-185">a.</span></span> <span data-ttu-id="51fb7-186">In de **beschrijving** textbox type `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="51fb7-186">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="51fb7-187">b.</span><span class="sxs-lookup"><span data-stu-id="51fb7-187">b.</span></span> <span data-ttu-id="51fb7-188">Als **verloopt**, selecteer **In 2 jaar**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="51fb7-189">c.</span><span class="sxs-lookup"><span data-stu-id="51fb7-189">c.</span></span> <span data-ttu-id="51fb7-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="51fb7-190">Click **Save**.</span></span>

    <span data-ttu-id="51fb7-191">d.</span><span class="sxs-lookup"><span data-stu-id="51fb7-191">d.</span></span> <span data-ttu-id="51fb7-192">Kopieer de waarde van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="51fb7-192">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="51fb7-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51fb7-193">Next Steps</span></span>
* <span data-ttu-id="51fb7-194">Wilt u de toegang tot de gegevens van de Azure AD rapportage-API op een programmatische manier?</span><span class="sxs-lookup"><span data-stu-id="51fb7-194">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="51fb7-195">Bekijk [aan de slag met Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="51fb7-195">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="51fb7-196">Als u meer informatie over Azure Active Directory-rapportage wilt, raadpleegt u de [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="51fb7-196">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

