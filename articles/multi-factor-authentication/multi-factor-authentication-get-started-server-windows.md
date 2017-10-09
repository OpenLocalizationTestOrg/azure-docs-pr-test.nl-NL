---
title: aaaWindows verificatie en Azure MFA-Server | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina die u helpt bij het implementeren van Windows-verificatie en Azure multi-factor Authentication-Server.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="95e80-103">Windows-verificatie en Azure Multi-Factor Authentication-server</span><span class="sxs-lookup"><span data-stu-id="95e80-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="95e80-104">Sectie van de Windows-verificatie Hallo van hello Azure multi-factor Authentication-Server tooenable gebruik en configureren van Windows-verificatie voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="95e80-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="95e80-105">Voordat u Windows-verificatie instellen, houd Hallo lijst rekening te volgen:</span><span class="sxs-lookup"><span data-stu-id="95e80-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="95e80-106">Na de installatie opnieuw worden opgestart hello Azure multi-factor Authentication voor Terminal Services tootake effect.</span><span class="sxs-lookup"><span data-stu-id="95e80-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="95e80-107">Als 'Overeenkomende Azure multi-factor Authentication-gebruiker vereisen' is ingeschakeld en u zich niet in de gebruikerslijst hello, zich u niet kunnen toolog naar Hallo machine na opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="95e80-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="95e80-108">Goedgekeurde dat IP-adressen is afhankelijk van of de toepassing hello Hallo client-IP-met Hallo-verificatie kan bieden.</span><span class="sxs-lookup"><span data-stu-id="95e80-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="95e80-109">Momenteel wordt alleen Terminal Services ondersteund.</span><span class="sxs-lookup"><span data-stu-id="95e80-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="95e80-110">Deze functie is geen ondersteunde toosecure Terminal Services in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="95e80-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="95e80-111">toosecure een toepassing met de Windows-verificatie, gebruik Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="95e80-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="95e80-112">Klik op Hallo Windows-verificatie pictogram hello Azure multi-factor Authentication-Server.</span><span class="sxs-lookup"><span data-stu-id="95e80-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="95e80-113">![Windows-verificatie](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="95e80-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="95e80-114">Controleer de Hallo **Windows-verificatie inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="95e80-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="95e80-115">Dit selectievakje is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="95e80-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="95e80-116">Hallo op het tabblad toepassingen kan Hallo beheerder tooconfigure een of meer toepassingen voor Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="95e80-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="95e80-117">Selecteer een server of toepassing – opgeven of Hallo servertoepassing is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="95e80-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="95e80-118">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="95e80-118">Click **OK**.</span></span>
5. <span data-ttu-id="95e80-119">Klik op **Toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="95e80-119">Click **Add…**</span></span>
6. <span data-ttu-id="95e80-120">Hallo goedgekeurde IP-adressen tabblad kunt u tooskip Azure multi-factor Authentication voor Windows-sessies die afkomstig zijn van specifieke IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="95e80-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="95e80-121">Bijvoorbeeld, als beslissen werknemers gebruiken toepassing hello van Hallo kantoor of thuis, u dat u niet wilt dat hun telefoons voor Azure multi-factor Authentication terwijl ze op Hallo office overbodig.</span><span class="sxs-lookup"><span data-stu-id="95e80-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="95e80-122">Hiervoor geeft u het subnet van kantoor Hallo als goedgekeurde IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="95e80-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="95e80-123">Klik op **Toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="95e80-123">Click **Add…**</span></span>
8. <span data-ttu-id="95e80-124">Selecteer **één IP-adres** indien tooskip één IP-adres gewenst.</span><span class="sxs-lookup"><span data-stu-id="95e80-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="95e80-125">Selecteer **IP-bereik** indien tooskip gehele IP-bereik gewenst.</span><span class="sxs-lookup"><span data-stu-id="95e80-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="95e80-126">Voorbeeld 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="95e80-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="95e80-127">Selecteer **Subnet** indien toospecify een bereik gewenst van IP-adressen met subnetnotatie.</span><span class="sxs-lookup"><span data-stu-id="95e80-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="95e80-128">Geef IP-beginadres van Hallo-subnet en kies vervolgens Hallo relevante netmasker in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="95e80-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="95e80-129">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="95e80-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95e80-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95e80-130">Next steps</span></span>

- [<span data-ttu-id="95e80-131">VPN-apparaten van derden configureren voor Azure MFA Server</span><span class="sxs-lookup"><span data-stu-id="95e80-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="95e80-132">Uitbreiden van uw bestaande infrastructuur voor verificatie met Hallo NPS-extensie voor Azure MFA</span><span class="sxs-lookup"><span data-stu-id="95e80-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
