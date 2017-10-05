---
title: Een aangepaste domeinnaam configureren in Azure App Service (GoDaddy)
description: Informatie over het gebruik van een domeinnaam van GoDaddy met Azure-Web-Apps
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="43051-103">Een aangepaste domeinnaam configureren in Azure App Service configureren (rechtstreeks van GoDaddy gekocht)</span><span class="sxs-lookup"><span data-stu-id="43051-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="43051-104">Als u verwijzen naar de laatste stap van het domein via Azure App Service Web Apps hebt aangeschaft [domein kopen voor Web-Apps](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="43051-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="43051-105">In dit artikel bevat instructies over het gebruik van een aangepaste domeinnaam die is gekocht rechtstreeks vanuit [GoDaddy](https://godaddy.com) met [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="43051-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="43051-106">Informatie over DNS-records</span><span class="sxs-lookup"><span data-stu-id="43051-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="43051-107">Een DNS-record voor uw aangepaste domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="43051-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="43051-108">Uw aangepaste domein koppelt u een web-app in App Service, moet u een nieuwe vermelding in de DNS-tabel voor uw aangepaste domein toevoegen met behulp van hulpprogramma's van GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="43051-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="43051-109">Gebruik de volgende stappen om te vinden van de DNS-hulpprogramma's voor GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="43051-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="43051-110">Aanmelden bij uw account met GoDaddy.com en selecteer **Mijn Account** en vervolgens **mijn domeinen beheren**.</span><span class="sxs-lookup"><span data-stu-id="43051-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="43051-111">Selecteer de vervolgkeuzelijst voor de domeinnaam die u wilt gebruiken met uw Azure-web-app en selecteer **beheren DNS-**.</span><span class="sxs-lookup"><span data-stu-id="43051-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![de pagina aangepast domein voor GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="43051-113">Van de **domein details** pagina, bladert u naar de **DNS-zonebestand** tabblad.</span><span class="sxs-lookup"><span data-stu-id="43051-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="43051-114">Dit is de sectie die is gebruikt voor het toevoegen en wijzigen van DNS-records voor uw domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="43051-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Tabblad DNS-zonebestand](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="43051-116">Selecteer **Record toevoegen** een bestaande record toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="43051-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="43051-117">Naar **bewerken** een bestaande record, selecteer de pen & papier: het pictogram naast de record.</span><span class="sxs-lookup"><span data-stu-id="43051-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="43051-118">Voordat u nieuwe records toevoegt, houd er rekening mee dat de GoDaddy al DNS-records voor populaire subdomeinen heeft gemaakt (aangeroepen **Host** in de editor) zoals **e**, **bestanden**, **mail**, en andere.</span><span class="sxs-lookup"><span data-stu-id="43051-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="43051-119">Als de naam die u wilt gebruiken, al bestaat, wijzigt u de bestaande record in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="43051-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="43051-120">Wanneer u een record toevoegt, moet u eerst het recordtype selecteren.</span><span class="sxs-lookup"><span data-stu-id="43051-120">When adding a record, you must first select the record type.</span></span>
   
    ![Selecteer recordtype](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="43051-122">Vervolgens moet u opgeven de **Host** (het aangepaste domein of de subdomeinnaam) en wat de it **verwijst naar**.</span><span class="sxs-lookup"><span data-stu-id="43051-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![zone-record toevoegen](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="43051-124">Bij het toevoegen van een **A-record (host)** -stelt u de **Host** naar elk veld  **@**  (Hiermee hoofddomeinnaam, zoals **contoso.com** ,) * (een jokerteken voor meerdere subdomeinen overeenkomende) of het onderliggende domein dat u wilt gebruiken (bijvoorbeeld **www**.) U moet instellen de **verwijst naar** veld in de IP-adres van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="43051-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="43051-125">Bij het toevoegen van een **(alias) CNAME-record** -stelt u de **Host** veld met het onderliggende domein dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="43051-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="43051-126">Bijvoorbeeld: **www**.</span><span class="sxs-lookup"><span data-stu-id="43051-126">For example, **www**.</span></span> <span data-ttu-id="43051-127">U moet instellen de **verwijst naar** veld de **. azurewebsites.net** domeinnaam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="43051-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="43051-128">Bijvoorbeeld: **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="43051-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="43051-129">Klik op **toevoegen van een andere**.</span><span class="sxs-lookup"><span data-stu-id="43051-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="43051-130">Selecteer **TXT** als het recordtype geeft een **Host** waarde van  **@**  en een **verwijst naar** waarde van  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="43051-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="43051-131">Deze TXT-record wordt gebruikt door Azure valideren waarvan u eigenaar van het domein dat is beschreven door de A-record of de eerste TXT-record.</span><span class="sxs-lookup"><span data-stu-id="43051-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="43051-132">Als het domein is toegewezen aan de web-app in de Azure Portal, kan dit TXT-record item worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="43051-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="43051-133">Wanneer u klaar bent met het toevoegen of wijzigen van records, klikt u op **voltooien** wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="43051-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="43051-134">De naam van het domein op uw web-app inschakelen</span><span class="sxs-lookup"><span data-stu-id="43051-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="43051-135">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="43051-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="43051-136">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="43051-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="43051-137">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="43051-137">What's changed</span></span>
* <span data-ttu-id="43051-138">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="43051-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

