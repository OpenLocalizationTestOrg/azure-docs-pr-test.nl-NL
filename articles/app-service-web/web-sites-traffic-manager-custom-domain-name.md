---
title: Een aangepaste domeinnaam voor een web-app in Azure App Service die gebruikmaakt van Traffic Manager voor taakverdeling configureren.
description: Gebruik een aangepaste domeinnaam voor een een web-app in Azure App Service met Traffic Manager voor taakverdeling.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 5f099201d9018a6f8577cb3daf127d09560fb94b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="e2041-103">Configureren van een aangepaste domeinnaam voor een web-app in Azure App Service met behulp van Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e2041-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="e2041-104">Dit artikel bevat algemene instructies voor het gebruik van een aangepaste domeinnaam met Azure App Service die Traffic Manager voor taakverdeling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2041-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="e2041-105">Informatie over DNS-records</span><span class="sxs-lookup"><span data-stu-id="e2041-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="e2041-106">Configureren van uw web-apps voor standaardmodus</span><span class="sxs-lookup"><span data-stu-id="e2041-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="e2041-107">Een DNS-record voor uw aangepaste domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="e2041-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="e2041-108">Als u domein via Azure App Service Web Apps hebt aangeschaft en overslaan van de volgende stappen uit en naar de laatste stap van verwijzen [domein kopen voor Web-Apps](custom-dns-web-site-buydomains-web-app.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e2041-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="e2041-109">Uw aangepaste domein koppelt u een web-app in Azure App Service, moet u een nieuwe vermelding in de DNS-tabel voor uw aangepaste domein toevoegen met behulp van hulpprogramma's van de domeinregistrar die u hebt aangeschaft met de domeinnaam van uw uit.</span><span class="sxs-lookup"><span data-stu-id="e2041-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="e2041-110">Gebruik de volgende stappen uit om te zoeken en de DNS-hulpprogramma's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2041-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="e2041-111">Aanmelden bij uw account bij uw domeinregistrar en zoekt u naar een pagina voor het beheren van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="e2041-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="e2041-112">Zoek naar koppelingen of gebieden van de site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="e2041-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="e2041-113">Vaak een koppeling naar deze pagina vindt u gegevens over uw account weer te geven en te zoeken naar een koppeling zoals **mijn domeinen**.</span><span class="sxs-lookup"><span data-stu-id="e2041-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="e2041-114">Wanneer u de beheerpagina hebt gevonden voor de domeinnaam, zoekt u een koppeling waarmee u de DNS-records bewerken.</span><span class="sxs-lookup"><span data-stu-id="e2041-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="e2041-115">Dit worden vermeld als een **zonebestand**, **DNS-Records**, of als een **Geavanceerd** configuratiekoppeling.</span><span class="sxs-lookup"><span data-stu-id="e2041-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="e2041-116">De pagina heeft hoogstwaarschijnlijk een aantal records dat al is gemaakt, zoals het koppelen van een vermelding '**@**'of'\*' met een pagina 'domein parkeerplaatsen'.</span><span class="sxs-lookup"><span data-stu-id="e2041-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="e2041-117">Records voor algemene subdomeinen kunnen ook zoals bevatten **www**.</span><span class="sxs-lookup"><span data-stu-id="e2041-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="e2041-118">De pagina wordt vermeld **CNAME-records**, of geef een vervolgkeuzelijst om te selecteren van een recordtype.</span><span class="sxs-lookup"><span data-stu-id="e2041-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="e2041-119">Het kan ook andere records, zoals vermeld **A-records** en **MX-records**.</span><span class="sxs-lookup"><span data-stu-id="e2041-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="e2041-120">In sommige gevallen CNAME-records wordt aangeroepen door andere namen, zoals een **Alias-Record**.</span><span class="sxs-lookup"><span data-stu-id="e2041-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="e2041-121">De pagina heeft de velden waarmee u kunt ook **kaart** van een **hostnaam** of **domeinnaam** naar een andere domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="e2041-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="e2041-122">Terwijl de details van elke registrar variëren, in het algemeen u toewijzen *van* uw aangepaste domeinnaam (zoals **contoso.com**,) *naar* de naam van het Traffic Manager-domein (**contoso.trafficmanager.net**) die voor uw web-app wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2041-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e2041-123">Als een record al in gebruik is en u moet uw apps optie preventief binden aan, kunt u ook een extra CNAME-record maken.</span><span class="sxs-lookup"><span data-stu-id="e2041-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="e2041-124">Bijvoorbeeld, optie preventief binden **www.contoso.com** aan uw web-app maakt u een CNAME-record van **awverify.www** naar **contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="e2041-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="e2041-125">U kunt vervolgens 'www.contoso.com' toevoegen aan uw Web-App zonder te wijzigen van de 'www' CNAME-record.</span><span class="sxs-lookup"><span data-stu-id="e2041-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="e2041-126">Zie voor meer informatie [maken DNS-records voor een web-app in een aangepast domein][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="e2041-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="e2041-127">Zodra u klaar bent met het toevoegen of wijzigen van DNS-records bij uw registrar, moet u de wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="e2041-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="e2041-128">Traffic Manager inschakelen</span><span class="sxs-lookup"><span data-stu-id="e2041-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="e2041-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2041-129">Next steps</span></span>
<span data-ttu-id="e2041-130">Zie het [Node.js Developer Center](/develop/nodejs/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2041-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
