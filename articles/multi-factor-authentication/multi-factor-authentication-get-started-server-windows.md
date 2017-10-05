---
title: Windows-verificatie en Azure MFA-server | Microsoft Docs
description: Dit is de Azure Multi-Factor Authentication-pagina die u helpt bij het implementeren van Windows-verificatie en de Azure Multi-Factor Authentication-server.
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
ms.openlocfilehash: 7e6384ea8fea686b5cad1a3bc3007252b9cfcd65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="853d4-103">Windows-verificatie en Azure Multi-Factor Authentication-server</span><span class="sxs-lookup"><span data-stu-id="853d4-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="853d4-104">Gebruik de Windows-verificatiesectie van de Azure Multi-Factor Authentication-server om Windows-verificatie in te schakelen en te configureren voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="853d4-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="853d4-105">Raadpleeg de volgende lijst voordat u Windows-verificatie instelt:</span><span class="sxs-lookup"><span data-stu-id="853d4-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="853d4-106">Start na de installatie Azure Multi-Factor Authentication opnieuw op om Terminal Services te activeren.</span><span class="sxs-lookup"><span data-stu-id="853d4-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="853d4-107">Als 'Overeenkomende Azure Multi-Factor Authentication-gebruiker vereisen' is ingeschakeld en u niet voorkomt in de lijst met gebruikers, kunt u zich niet aanmelden bij de computer wanneer deze opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="853d4-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="853d4-108">Goedgekeurde IP-adressen is afhankelijk van de vraag of de toepassing de client-IP kan aanbieden bij de verificatie.</span><span class="sxs-lookup"><span data-stu-id="853d4-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="853d4-109">Momenteel wordt alleen Terminal Services ondersteund.</span><span class="sxs-lookup"><span data-stu-id="853d4-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="853d4-110">Deze functie wordt niet ondersteund om Terminal Services op Windows Server 2012 R2 te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="853d4-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="853d4-111">Gebruik de volgende procedure als u een toepassing met Windows-verificatie wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="853d4-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="853d4-112">Klik in de Azure Multi-Factor Authentication-server op het pictogram Windows-authenticatie.</span><span class="sxs-lookup"><span data-stu-id="853d4-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="853d4-113">![Windows-verificatie](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="853d4-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="853d4-114">Schakel het selectievakje **Windows-verificatie** in.</span><span class="sxs-lookup"><span data-stu-id="853d4-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="853d4-115">Dit selectievakje is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="853d4-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="853d4-116">Op het tabblad Toepassingen kan de beheerder een of meer toepassingen configureren voor Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="853d4-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="853d4-117">Selecteer een server of toepassing. Geef op of de server/toepassing is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="853d4-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="853d4-118">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="853d4-118">Click **OK**.</span></span>
5. <span data-ttu-id="853d4-119">Klik op **Toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="853d4-119">Click **Add…**</span></span>
6. <span data-ttu-id="853d4-120">Op het tabblad Goedgekeurde IP-adressen kunt u Azure Multi-Factor Authentication voor Windows-sessies die afkomstig zijn van specifieke IP-adressen overslaan.</span><span class="sxs-lookup"><span data-stu-id="853d4-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="853d4-121">Als werknemers bijvoorbeeld de toepassing zowel op kantoor als thuis gebruiken, kunt u instellen dat hun telefoons voor Azure Multi-Factor Authentication niet overgaan wanneer ze op kantoor zijn.</span><span class="sxs-lookup"><span data-stu-id="853d4-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="853d4-122">Hiervoor geeft u het subnet van de werkplek op als een van de goedgekeurde IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="853d4-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="853d4-123">Klik op **Toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="853d4-123">Click **Add…**</span></span>
8. <span data-ttu-id="853d4-124">Selecteer **Eén IP-adres** als u één IP-adres wilt overslaan.</span><span class="sxs-lookup"><span data-stu-id="853d4-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="853d4-125">Selecteer **IP-bereik** als u een heel IP-adresbereik wilt overslaan.</span><span class="sxs-lookup"><span data-stu-id="853d4-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="853d4-126">Voorbeeld 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="853d4-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="853d4-127">Selecteer **Subnet** als u een bereik van IP-adressen wilt opgeven met subnetnotatie.</span><span class="sxs-lookup"><span data-stu-id="853d4-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="853d4-128">Voer het IP-adres in waarop het subnet begint en kies het juiste IP-masker uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="853d4-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="853d4-129">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="853d4-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="853d4-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="853d4-130">Next steps</span></span>

- [<span data-ttu-id="853d4-131">VPN-apparaten van derden configureren voor Azure MFA Server</span><span class="sxs-lookup"><span data-stu-id="853d4-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="853d4-132">De bestaande infrastructuur voor verificatie uitbreiden met de NPS-extensie voor Azure MFA</span><span class="sxs-lookup"><span data-stu-id="853d4-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
