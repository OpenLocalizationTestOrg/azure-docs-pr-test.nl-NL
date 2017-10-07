---
title: aaaConfigure een aangepaste domeinnaam voor een web-app in Azure App Service die gebruikmaakt van Traffic Manager voor taakverdeling.
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
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="a957e-103">Configureren van een aangepaste domeinnaam voor een web-app in Azure App Service met behulp van Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a957e-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="a957e-104">Dit artikel bevat algemene instructies voor het gebruik van een aangepaste domeinnaam met Azure App Service die Traffic Manager voor taakverdeling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a957e-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="a957e-105">Informatie over DNS-records</span><span class="sxs-lookup"><span data-stu-id="a957e-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="a957e-106">Configureren van uw web-apps voor standaardmodus</span><span class="sxs-lookup"><span data-stu-id="a957e-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="a957e-107">Een DNS-record voor uw aangepaste domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="a957e-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="a957e-108">Als u domein via Azure App Service Web Apps hebt aangeschaft en vervolgens overslaat stappen uit te voeren en raadpleegt u de laatste stap toohello van [domein kopen voor Web-Apps](custom-dns-web-site-buydomains-web-app.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a957e-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="a957e-109">tooassociate uw aangepaste domein met een web-app in Azure App Service, moet u een nieuwe vermelding toevoegen in Hallo DNS-tabel voor uw aangepaste domein met behulp van hulpprogramma's van Hallo domeinregistrar die u hebt aangeschaft met de domeinnaam van uw uit.</span><span class="sxs-lookup"><span data-stu-id="a957e-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="a957e-110">Gebruik Hallo toolocate stappen te volgen en Hallo DNS-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="a957e-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="a957e-111">Meld u aan bij uw domeinregistrar tooyour-account en zoekt u naar een pagina voor het beheren van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="a957e-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="a957e-112">Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="a957e-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="a957e-113">Vaak een koppeling toothis pagina vindt u gegevens over uw account weer te geven en te zoeken naar een koppeling zoals **mijn domeinen**.</span><span class="sxs-lookup"><span data-stu-id="a957e-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="a957e-114">Wanneer u Hallo management-pagina voor de domeinnaam gevonden hebt, zoekt u een koppeling waarmee u tooedit Hallo DNS-records.</span><span class="sxs-lookup"><span data-stu-id="a957e-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="a957e-115">Dit worden vermeld als een **zonebestand**, **DNS-Records**, of als een **Geavanceerd** configuratiekoppeling.</span><span class="sxs-lookup"><span data-stu-id="a957e-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="a957e-116">Hallo-pagina heeft hoogstwaarschijnlijk een aantal records dat al is gemaakt, zoals het koppelen van een vermelding '**@**'of'\*' met een pagina 'domein parkeerplaatsen'.</span><span class="sxs-lookup"><span data-stu-id="a957e-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="a957e-117">Records voor algemene subdomeinen kunnen ook zoals bevatten **www**.</span><span class="sxs-lookup"><span data-stu-id="a957e-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="a957e-118">Hallo-pagina wordt vermeld **CNAME-records**, of geef een vervolgkeuzelijst tooselect een recordtype.</span><span class="sxs-lookup"><span data-stu-id="a957e-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="a957e-119">Het kan ook andere records, zoals vermeld **A-records** en **MX-records**.</span><span class="sxs-lookup"><span data-stu-id="a957e-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="a957e-120">In sommige gevallen CNAME-records wordt aangeroepen door andere namen, zoals een **Alias-Record**.</span><span class="sxs-lookup"><span data-stu-id="a957e-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="a957e-121">Hallo-pagina heeft ook velden die u in te stellen**kaart** van een **hostnaam** of **domeinnaam** tooanother domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="a957e-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="a957e-122">Tijdens het Hallo-details van elke registrar variëren, in het algemeen u toewijzen *van* uw aangepaste domeinnaam (zoals **contoso.com**,) *naar* Hallo Traffic Manager-domeinnaam (**contoso.trafficmanager.net**) die voor uw web-app wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a957e-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a957e-123">U kunt ook als een record is al in gebruik en u moet toopreemptively binden van uw apps tooit, kunt u een extra CNAME-record maken.</span><span class="sxs-lookup"><span data-stu-id="a957e-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="a957e-124">Bijvoorbeeld: toopreemptively bind **www.contoso.com** tooyour web-app, maakt u een CNAME-record van **awverify.www** te**contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="a957e-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="a957e-125">U kunt vervolgens 'www.contoso.com' tooyour Web-App toevoegen zonder Hallo 'www' CNAME-record.</span><span class="sxs-lookup"><span data-stu-id="a957e-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="a957e-126">Zie voor meer informatie [maken DNS-records voor een web-app in een aangepast domein][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="a957e-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="a957e-127">Zodra u klaar bent met het toevoegen of wijzigen van DNS-records bij uw registrar, sla de wijzigingen van Hallo.</span><span class="sxs-lookup"><span data-stu-id="a957e-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="a957e-128">Traffic Manager inschakelen</span><span class="sxs-lookup"><span data-stu-id="a957e-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="a957e-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a957e-129">Next steps</span></span>
<span data-ttu-id="a957e-130">Zie voor meer informatie, Hallo [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="a957e-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
