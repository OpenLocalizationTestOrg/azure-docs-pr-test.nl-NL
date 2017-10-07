---
title: aaaEnabling end tooend SSL op Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo Application Gateway end tooend ondersteuning voor SSL.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a><span data-ttu-id="9186c-103">Overzicht van end tooend SSL met Application Gateway</span><span class="sxs-lookup"><span data-stu-id="9186c-103">Overview of end tooend SSL with Application Gateway</span></span>

<span data-ttu-id="9186c-104">Toepassingsgateway biedt ondersteuning voor SSL-beëindiging aan Hallo-gateway, na welk verkeer stroomt doorgaans niet-versleuteld toohello back-endservers.</span><span class="sxs-lookup"><span data-stu-id="9186c-104">Application gateway supports SSL termination at hello gateway, after which traffic typically flows unencrypted toohello backend servers.</span></span> <span data-ttu-id="9186c-105">Deze functie kunt web servers toobe unburdened van dure versleuteling en ontsleuteling overhead.</span><span class="sxs-lookup"><span data-stu-id="9186c-105">This feature allows web servers toobe unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="9186c-106">Voor sommige klanten echter is het niet-versleutelde communicatie toohello back-endservers geen acceptabele optie.</span><span class="sxs-lookup"><span data-stu-id="9186c-106">However for some customers unencrypted communication toohello backend servers is not an acceptable option.</span></span> <span data-ttu-id="9186c-107">Deze niet-versleutelde communicatie kan vanwege toosecurity vereisten, nalevingsvereisten, of Hallo-toepassing kan alleen een beveiligde verbinding accepteren.</span><span class="sxs-lookup"><span data-stu-id="9186c-107">This unencrypted communication could be due toosecurity requirements, compliance requirements, or hello application may only accept a secure connection.</span></span> <span data-ttu-id="9186c-108">Voor dergelijke toepassingen ondersteunt toepassingsgateway end tooend SSL versleuteling.</span><span class="sxs-lookup"><span data-stu-id="9186c-108">For such applications, application gateway supports end tooend SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="9186c-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9186c-109">Overview</span></span>

<span data-ttu-id="9186c-110">Einde tooend SSL kunt u toosecurely verzenden gevoelige gegevens toohello back-end versleuteld terwijl nog steeds profiteren van de voordelen van de functies voor taakverdeling laag 7 Hallo welke toepassingsgateway bevat.</span><span class="sxs-lookup"><span data-stu-id="9186c-110">End tooend SSL allows you toosecurely transmit sensitive data toohello backend encrypted while still taking advantage of hello benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="9186c-111">Sommige van deze functies zijn sessie cookies gebaseerde affiniteit, URL gebaseerde routering, ondersteuning voor routering op basis van sites of mogelijkheid tooinject X - doorgestuurd-* headers.</span><span class="sxs-lookup"><span data-stu-id="9186c-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability tooinject X-Forwarded-* headers.</span></span>

<span data-ttu-id="9186c-112">Wanneer met einde tooend SSL-communicatie-modus is geconfigureerd, wordt toepassingsgateway beëindigt Hallo SSL-sessies op Hallo-gateway en gebruikersverkeer ontsleutelt.</span><span class="sxs-lookup"><span data-stu-id="9186c-112">When configured with end tooend SSL communication mode, application gateway terminates hello SSL sessions at hello gateway and decrypts user traffic.</span></span> <span data-ttu-id="9186c-113">Het is van toepassing hello geconfigureerd regels tooselect een geschikte back-end groep exemplaar tooroute verkeer naar.</span><span class="sxs-lookup"><span data-stu-id="9186c-113">It then applies hello configured rules tooselect an appropriate backend pool instance tooroute traffic to.</span></span> <span data-ttu-id="9186c-114">Toepassingsgateway vervolgens een nieuwe SSL-verbinding toohello back-endserver initieert en opnieuw versleutelt gegevens met behulp van de openbare-sleutelcertificaat Hallo back-end van de server voordat het Hallo-aanvraag toohello back-end verzendt.</span><span class="sxs-lookup"><span data-stu-id="9186c-114">Application gateway then initiates a new SSL connection toohello backend server and re-encrypts data using hello backend server's public key certificate before transmitting hello request toohello backend.</span></span> <span data-ttu-id="9186c-115">Einde tooend die SSL is ingeschakeld protocolinstelling door in te stellen BackendHTTPSetting tooHTTPS, die vervolgens toegepast tooa back-endpool.</span><span class="sxs-lookup"><span data-stu-id="9186c-115">End tooend SSL is enabled by setting protocol setting in BackendHTTPSetting tooHTTPS, which is then applied tooa backend pool.</span></span> <span data-ttu-id="9186c-116">Elke back-endserver in de back-endpool Hallo met einde tooend die SSL ingeschakeld moet worden geconfigureerd met een certificaat tooallow veilige communicatie.</span><span class="sxs-lookup"><span data-stu-id="9186c-116">Each backend server in hello backend pool with end tooend SSL enabled must be configured with a certificate tooallow secure communication.</span></span>

![einde tooend ssl scenario][1]

<span data-ttu-id="9186c-118">In dit voorbeeld worden aanvragen TLS1.2 via gerouteerde toobackend-servers in Pool1 end tooend SSL gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9186c-118">In this example, requests using TLS1.2 are routed toobackend servers in Pool1 using end tooend SSL.</span></span>

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="9186c-119">End tooend SSL en whitelisting van certificaten</span><span class="sxs-lookup"><span data-stu-id="9186c-119">End tooend SSL and whitelisting of certificates</span></span>

<span data-ttu-id="9186c-120">Toepassingsgateway communiceert alleen met bekende back-end-instanties die goedgekeurde lijst hun certificaat met de toepassingsgateway Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="9186c-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with hello application gateway.</span></span> <span data-ttu-id="9186c-121">tooenable whitelisting van certificaten, moet u de openbare sleutel Hallo van back-end server certificaten toohello toepassingsgateway (geen basiscertificaat Hallo) uploaden.</span><span class="sxs-lookup"><span data-stu-id="9186c-121">tooenable whitelisting of certificates, you must upload hello public key of backend server certificates toohello application gateway (not hello root certificate).</span></span> <span data-ttu-id="9186c-122">Alleen verbindingen tooknown en goedgekeurde lijst back-ends zijn vervolgens toegestaan.</span><span class="sxs-lookup"><span data-stu-id="9186c-122">Only connections tooknown and whitelisted backends are then allowed.</span></span> <span data-ttu-id="9186c-123">back-ends resterende Hallo resulteert in een gateway-fout.</span><span class="sxs-lookup"><span data-stu-id="9186c-123">hello remaining backends results in a gateway error.</span></span> <span data-ttu-id="9186c-124">Zelfondertekende certificaten zijn uitsluitend bedoeld voor testdoeleinden en het wordt afgeraden om deze in een productieomgeving te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9186c-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="9186c-125">Deze certificaten hebben toobe goedgekeurde lijst met Hallo toepassingsgateway zoals beschreven in Hallo vorige stappen voordat ze kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9186c-125">Such certificates have toobe whitelisted with hello application gateway as described in hello preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9186c-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9186c-126">Next steps</span></span>

<span data-ttu-id="9186c-127">Nadat u hebt leren over end tooend SSL gaat te[end tooend SSL in toepassingsgateway inschakelen](application-gateway-end-to-end-ssl-powershell.md) toocreate wordt gebruikt door een toepassing gateway eindigen tooend SSL.</span><span class="sxs-lookup"><span data-stu-id="9186c-127">After learning about end tooend SSL, go too[enable end tooend SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) toocreate an application gateway using end tooend SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
