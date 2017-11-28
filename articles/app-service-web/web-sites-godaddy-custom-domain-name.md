---
title: aaaConfigure een aangepaste domeinnaam in Azure App Service (GoDaddy)
description: Meer informatie over hoe een domein toouse naam uit GoDaddy met Azure-Web-Apps
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
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="488cc-103">Een aangepaste domeinnaam configureren in Azure App Service configureren (rechtstreeks van GoDaddy gekocht)</span><span class="sxs-lookup"><span data-stu-id="488cc-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="488cc-104">Als u een domein via Azure App Service Web Apps hebt aangeschaft vervolgens raadpleegt u de laatste stap toohello van [domein kopen voor Web-Apps](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="488cc-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="488cc-105">In dit artikel bevat instructies over het gebruik van een aangepaste domeinnaam die is gekocht rechtstreeks vanuit [GoDaddy](https://godaddy.com) met [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="488cc-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="488cc-106">Informatie over DNS-records</span><span class="sxs-lookup"><span data-stu-id="488cc-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="488cc-107">Een DNS-record voor uw aangepaste domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="488cc-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="488cc-108">tooassociate uw aangepaste domein met een web-app in App Service, moet u een nieuwe vermelding toevoegen in Hallo DNS-tabel voor uw aangepaste domein met behulp van hulpprogramma's van GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="488cc-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="488cc-109">Volgende stappen toolocate Hallo DNS-hulpprogramma's voor GoDaddy.com hello gebruiken</span><span class="sxs-lookup"><span data-stu-id="488cc-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="488cc-110">Meld u aan tooyour-account met GoDaddy.com en selecteer **Mijn Account** en vervolgens **mijn domeinen beheren**.</span><span class="sxs-lookup"><span data-stu-id="488cc-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="488cc-111">Selecteer Hallo vervolgkeuzelijst voor Hallo-domeinnaam die u toouse met uw Azure-web-app wilt en selecteer **beheren DNS-**.</span><span class="sxs-lookup"><span data-stu-id="488cc-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![de pagina aangepast domein voor GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="488cc-113">Van Hallo **domein details** pagina, schuiven toohello **DNS-zonebestand** tabblad. Dit is gebruikt voor het toevoegen en wijzigen van DNS-records voor uw domeinnaam Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="488cc-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Tabblad DNS-zonebestand](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="488cc-115">Selecteer **Record toevoegen** tooadd een bestaande record.</span><span class="sxs-lookup"><span data-stu-id="488cc-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="488cc-116">te**bewerken** een bestaande record, selecteer Hallo pen en papier pictogram naast Hallo record.</span><span class="sxs-lookup"><span data-stu-id="488cc-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="488cc-117">Voordat u nieuwe records toevoegt, houd er rekening mee dat de GoDaddy al DNS-records voor populaire subdomeinen heeft gemaakt (aangeroepen **Host** in de editor) zoals **e**, **bestanden**, **mail**, en andere.</span><span class="sxs-lookup"><span data-stu-id="488cc-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="488cc-118">Als het Hallo-naam die u wenst dat toouse al bestaat, wijzigt u Hallo bestaande record in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="488cc-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="488cc-119">Wanneer u een record toevoegt, moet u eerst het recordtype Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="488cc-119">When adding a record, you must first select hello record type.</span></span>
   
    ![Selecteer recordtype](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="488cc-121">Vervolgens moet u opgeven Hallo **Host** (Hallo aangepast domein of subdomein) en wat de it **verwijst naar**.</span><span class="sxs-lookup"><span data-stu-id="488cc-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![zone-record toevoegen](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="488cc-123">Bij het toevoegen van een **A-record (host)** -u moet instellen Hallo **Host** veld tooeither  **@**  (Hiermee hoofddomeinnaam, zoals  **Contoso.com**,) * (een jokerteken voor meerdere subdomeinen overeenkomende) of subdomein hello gewenst toouse (bijvoorbeeld **www**.) U moet instellen Hallo **verwijst naar** veld toohello IP-adres van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="488cc-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="488cc-124">Bij het toevoegen van een **(alias) CNAME-record** -u moet instellen Hallo **Host** veld toohello subdomein gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="488cc-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="488cc-125">Bijvoorbeeld: **www**.</span><span class="sxs-lookup"><span data-stu-id="488cc-125">For example, **www**.</span></span> <span data-ttu-id="488cc-126">U moet instellen Hallo **verwijst naar** veld toohello **. azurewebsites.net** domeinnaam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="488cc-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="488cc-127">Bijvoorbeeld: **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="488cc-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="488cc-128">Klik op **toevoegen van een andere**.</span><span class="sxs-lookup"><span data-stu-id="488cc-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="488cc-129">Selecteer **TXT** als Hallo recordtype, Geef een **Host** waarde van  **@**  en een **verwijst naar** waarde van  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="488cc-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="488cc-130">Deze TXT-record wordt gebruikt door Azure toovalidate dat u bezit Hallo domein beschreven door Hallo een record of Hallo eerste TXT-record.</span><span class="sxs-lookup"><span data-stu-id="488cc-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="488cc-131">Als Hallo domein is toegewezen toohello web-app in Azure Portal hello, kan dit TXT-record item worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="488cc-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="488cc-132">Wanneer u klaar bent met het toevoegen of wijzigen van records, klikt u op **voltooien** toosave wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="488cc-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="488cc-133">Hallo-domeinnaam op uw web-app inschakelen</span><span class="sxs-lookup"><span data-stu-id="488cc-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="488cc-134">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="488cc-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="488cc-135">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="488cc-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="488cc-136">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="488cc-136">What's changed</span></span>
* <span data-ttu-id="488cc-137">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="488cc-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

