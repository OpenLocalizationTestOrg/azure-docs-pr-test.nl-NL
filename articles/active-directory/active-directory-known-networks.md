---
title: Netwerken bekend in de klassieke Azure portal | Microsoft Docs
description: Door bekende netwerken te configureren, kunt u te voorkomen dat IP-adressen die eigendom zijn van uw organisatie die is opgenomen in de modules aanmelding vanaf meerdere locaties en aanmelding aanmeldingen vanaf IP-adressen met verdachte activiteitsrapporten.
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="83b9b-103">Bekende netwerken</span><span class="sxs-lookup"><span data-stu-id="83b9b-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="83b9b-104">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="83b9b-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="83b9b-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="83b9b-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="83b9b-106">U kunt toegang tot Azure Active Directory- en gebruiksrapporten meer inzicht verkrijgen in de integriteit en beveiliging van de directory van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="83b9b-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="83b9b-107">Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's mogelijk liggen zodat ze voldoende plannen kunnen die risico's te beperken.</span><span class="sxs-lookup"><span data-stu-id="83b9b-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="83b9b-108">Het is mogelijk dat de '*aanmeldingen vanaf meerdere locaties*'en'*aanmeldingen vanaf IP-adressen met verdachte activiteit*' rapporten markeert IP-adressen die eigendom zijn door uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="83b9b-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="83b9b-109">Dit kan bijvoorbeeld gebeuren wanneer:</span><span class="sxs-lookup"><span data-stu-id="83b9b-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="83b9b-110">Een gebruiker in uw office is extern aangemeld bij uw datacenter in San Francisco Boston activeert het rapport 'Aanmeldingen vanaf meerdere locaties'</span><span class="sxs-lookup"><span data-stu-id="83b9b-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="83b9b-111">Een gebruiker van uw organisatie wil aanmelding meerdere keren met een onjuist wachtwoord triggers het rapport "Aanmeldingen vanaf IP-adressen met verdachte activiteit"</span><span class="sxs-lookup"><span data-stu-id="83b9b-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="83b9b-112">Om te voorkomen dat dergelijke gevallen misleidend beveiligingsrapporten genereren, moet u de bekende IP-adresbereiken toevoegen aan de lijst met het openbare IP-adres van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="83b9b-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="83b9b-113">Als u wilt toevoegen van uw organisatie openbare IP-adresbereiken, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="83b9b-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="83b9b-114">Aanmelding bij de [Azure-beheerportal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="83b9b-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="83b9b-115">Klik in het linkerdeelvenster op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83b9b-115">In the left pane, click **Active Directory**.</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="83b9b-117">In de **Directory** tabblad, selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="83b9b-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="83b9b-118">Klik in het menu bovenaan op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="83b9b-118">In the menu on the top, click **Configure**.</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="83b9b-120">Op het tabblad configureren, gaat u naar **uw organisaties openbare IP-adresbereiken**</span><span class="sxs-lookup"><span data-stu-id="83b9b-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="83b9b-122">Klik op **bekende IP-adresbereiken toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="83b9b-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="83b9b-123">Toevoegen van uw-adresbereiken in het dialoogvenster dat wordt weergegeven en klik vervolgens op de knop controleren wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="83b9b-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="83b9b-125">**Aanvullende bronnen:**</span><span class="sxs-lookup"><span data-stu-id="83b9b-125">**Additional resources:**</span></span>

* [<span data-ttu-id="83b9b-126">Uw toegangs- en gebruiksrapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="83b9b-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="83b9b-127">Aanmeldingen vanaf IP-adressen met verdachte activiteiten</span><span class="sxs-lookup"><span data-stu-id="83b9b-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="83b9b-128">Aanmeldingen vanaf meerdere locaties</span><span class="sxs-lookup"><span data-stu-id="83b9b-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

