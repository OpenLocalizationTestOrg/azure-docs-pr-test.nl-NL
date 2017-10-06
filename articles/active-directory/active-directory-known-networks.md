---
title: aaaKnown netwerken in de klassieke Azure-portal Hallo | Microsoft Docs
description: Door bekende netwerken te configureren, kunt u te voorkomen dat IP-adressen die eigendom zijn van uw organisatie die is opgenomen in Hallo aanmelding aanmeldingen vanaf meerdere locaties en aanmelding aanmeldingen vanaf IP-adressen met verdachte activiteitsrapporten.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="b23f5-103">Bekende netwerken</span><span class="sxs-lookup"><span data-stu-id="b23f5-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b23f5-104">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b23f5-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="b23f5-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b23f5-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="b23f5-106">U kunt toegang tot Azure Active Directory en gebruik rapporten toogain inzicht in Hallo integriteit en beveiliging van de directory van uw organisatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b23f5-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="b23f5-107">Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's zodat u ze kunnen toomitigate voldoende plannen die risico's kunnen liggen.</span><span class="sxs-lookup"><span data-stu-id="b23f5-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="b23f5-108">Het is mogelijk dat Hallo '*aanmeldingen vanaf meerdere locaties*'en'*aanmeldingen vanaf IP-adressen met verdachte activiteit*' rapporten markeert IP-adressen die eigendom zijn van uw de organisatie.</span><span class="sxs-lookup"><span data-stu-id="b23f5-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="b23f5-109">Dit kan bijvoorbeeld gebeuren wanneer:</span><span class="sxs-lookup"><span data-stu-id="b23f5-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="b23f5-110">Een gebruiker in uw kantoor Boston heeft op afstand tooyour datacenter in San Francisco triggers Hallo 'Aanmelding aanmeldingen vanaf meerdere locaties' rapport aangemeld</span><span class="sxs-lookup"><span data-stu-id="b23f5-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="b23f5-111">Een gebruiker van uw organisatie probeert toosign op meerdere keren met een onjuist wachtwoord triggers Hallo 'Aanmelding aanmeldingen vanaf IP-adressen met verdachte activiteit' rapport</span><span class="sxs-lookup"><span data-stu-id="b23f5-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="b23f5-112">tooprevent deze gevallen van genereren misleidend beveiliging rapporten, moet u de bekende IP-adresbereiken toohello adreslijst van het openbare IP-adres van uw organisatie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b23f5-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="b23f5-113">tooadd bereiken van het openbare IP-adres van uw organisatie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b23f5-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="b23f5-114">Eenmalige aanmelding toohello [Azure-beheerportal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b23f5-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="b23f5-115">Klik in het linkerdeelvenster Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b23f5-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="b23f5-117">In Hallo **Directory** tabblad, selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="b23f5-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="b23f5-118">Klik in het menu bovenaan Hallo Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="b23f5-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="b23f5-120">Op tabblad Hallo configureren, gaat u te**uw organisaties openbare IP-adresbereiken**</span><span class="sxs-lookup"><span data-stu-id="b23f5-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="b23f5-122">Klik op **bekende IP-adresbereiken toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b23f5-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="b23f5-123">Toevoegen van uw-adresbereiken in Hallo dialoogvenster dat wordt weergegeven en klik vervolgens op de knop controleren Hallo wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="b23f5-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="b23f5-125">**Aanvullende bronnen:**</span><span class="sxs-lookup"><span data-stu-id="b23f5-125">**Additional resources:**</span></span>

* [<span data-ttu-id="b23f5-126">Uw toegangs- en gebruiksrapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="b23f5-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="b23f5-127">Aanmeldingen vanaf IP-adressen met verdachte activiteiten</span><span class="sxs-lookup"><span data-stu-id="b23f5-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="b23f5-128">Aanmeldingen vanaf meerdere locaties</span><span class="sxs-lookup"><span data-stu-id="b23f5-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

