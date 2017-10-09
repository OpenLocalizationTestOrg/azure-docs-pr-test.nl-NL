---
title: Connector voor toepassingsproxy-Agent installeren aaaProblem Hallo | Microsoft Docs
description: Hoe tootroubleshoot problemen die u mogelijk Hallo face bij het installeren van Connector voor toepassingsproxy-Agent
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="c9ccb-103">Problemen bij het Hallo-Connector voor toepassingsproxy-Agent installeren</span><span class="sxs-lookup"><span data-stu-id="c9ccb-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="c9ccb-104">Microsoft AAD Application Proxy Connector is een onderdeel van het interne domein die gebruikmaakt van uitgaande verbindingen tooestablish Hallo connectiviteit uit Hallo cloud beschikbare eindpunt toohello interne domein.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="c9ccb-105">Algemene probleemgebieden met installatie van de Connector</span><span class="sxs-lookup"><span data-stu-id="c9ccb-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="c9ccb-106">Wanneer Hallo-installatie van een connector is mislukt, is Hallo hoofdoorzaak meestal een Hallo gebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="c9ccb-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="c9ccb-107">**Connectiviteit** – toocomplete een geslaagde installatie Hallo nieuwe connector behoeften tooregister en toekomstige vertrouwensgegevens tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="c9ccb-108">Dit wordt gedaan door verbinding te maken toohello AAD Application Proxy-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="c9ccb-109">**Vertrouwensrelatie tot stand brengen** – Hallo nieuwe connector maakt u een zelfondertekend certificaat en toohello cloudservice geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="c9ccb-110">**Verificatie van Hallo beheerder** – tijdens de installatie Hallo gebruiker referenties moet opgeven admin installatie toocomplete Hallo-Connector.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="c9ccb-111">Controleer of connectivity toohello Cloud Application Proxy-service en Microsoft Login pagina</span><span class="sxs-lookup"><span data-stu-id="c9ccb-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="c9ccb-112">**Doelstelling:** controleren die connector Hallo machine toohello AAD Application Proxy registratie eindpunt, evenals een aanmeldingspagina voor Microsoft verbinding kan maken.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="c9ccb-113">Open een browser en Ga naar toohello webpagina's te volgen: <https://aadap-portcheck.connectorporttest.msappproxy.net> , en controleert u dat Hallo connectiviteit tooCentral VS en VS-Oost datacenters met poort 9090 en 9091 werkt.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="c9ccb-114">Als een van deze poorten is niet geslaagd (geen een groen vinkje), Controleer of dat Hallo Firewall of back-end-proxy heeft \*. msappproxy.net met poort 9090 en 9091 correct gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="c9ccb-115">Open een browser (door tabs gescheiden) en Ga na webpagina toohello: <https://login.microsoftonline.com>, zorg ervoor dat u zich toothat pagina aanmelden kunt.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="c9ccb-116">Controleer of de Machine- en back-end-onderdelen ondersteund voor toepassingsproxy vertrouwensrelatie cert</span><span class="sxs-lookup"><span data-stu-id="c9ccb-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="c9ccb-117">**Doelstelling:** controleren of Hallo connector machine, back-end-proxy en firewall Hallo certificaat dat is gemaakt door de connector Hallo voor toekomstige vertrouwensrelatie kunnen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="c9ccb-118">Hallo-connector probeert een SHA512-certificaat dat wordt ondersteund door TLS1.2 toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="c9ccb-119">Als het Hallo-machine of Hallo back-endfirewall en proxy wordt niet ondersteund voor TLS1.2, Hallo installatie mislukken.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="c9ccb-120">**probleem met de Hallo tooresolve:**</span><span class="sxs-lookup"><span data-stu-id="c9ccb-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="c9ccb-121">Controleer of de machine Hallo ondersteunt TLS1.2 – TLS 1.2 moeten ondersteuning voor alle Windows-versies na 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="c9ccb-122">Als de computer van de connector van een versie van 2012 R2 of vóór is, zorg ervoor dat Hallo volgende KB op Hallo computer zijn geïnstalleerd: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="c9ccb-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="c9ccb-123">Neem contact op met de beheerder van uw netwerk en vraag tooverify dat Hallo back-end-proxy- en firewallservers niet SHA512 voor uitgaand verkeer blokkeren.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="c9ccb-124">Controleer of admin gebruikte tooinstall Hallo-connector</span><span class="sxs-lookup"><span data-stu-id="c9ccb-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="c9ccb-125">**Doelstelling:** controleren die Hallo-gebruiker die tooinstall Hallo-connector probeert is een beheerder met de juiste referenties.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="c9ccb-126">Hallo-gebruiker moet op dit moment een globale beheerder voor Hallo installatie toosucceed.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="c9ccb-127">**tooverify hello referenties zijn juist:**</span><span class="sxs-lookup"><span data-stu-id="c9ccb-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="c9ccb-128">Verbinding te maken met<https://login.microsoftonline.com> en Hallo dezelfde referenties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="c9ccb-129">Zorg ervoor dat het Hallo-aanmelding is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-129">Make sure hello login is successful.</span></span> <span data-ttu-id="c9ccb-130">U kunt Hallo gebruikersrol controleren door te gaan**Azure Active Directory**  - &gt; **gebruikers en groepen**  - &gt; **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="c9ccb-131">Selecteer uw gebruikersaccount, klikt u vervolgens 'Directory rol' in de resulterende Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="c9ccb-132">Controleer of die geselecteerde rol Hallo 'Globale beheerder'.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="c9ccb-133">Als u tooaccess van Hallo-pagina's langs deze stappen bent, bent u niet een globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="c9ccb-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9ccb-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9ccb-134">Next steps</span></span>
[<span data-ttu-id="c9ccb-135">Azure AD-toepassingsproxy connectors begrijpen</span><span class="sxs-lookup"><span data-stu-id="c9ccb-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
