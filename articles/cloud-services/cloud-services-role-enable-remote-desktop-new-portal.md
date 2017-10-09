---
title: aaaEnable verbinding met extern bureaublad voor een rol in Azure Cloud Services | Microsoft Docs
description: Hoe tooconfigure uw azure cloud service-toepassing tooallow extern bureaublad-verbindingen
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="f8353-103">Verbinding met extern bureaublad voor een rol in Azure Cloudservices inschakelen</span><span class="sxs-lookup"><span data-stu-id="f8353-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8353-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f8353-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="f8353-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f8353-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="f8353-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8353-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="f8353-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f8353-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="f8353-108">Extern bureaublad kunt u tooaccess Hallo bureaublad van een functie die wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f8353-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="f8353-109">U kunt een tootroubleshoot extern bureaublad-verbinding gebruiken en analyseren van problemen met uw toepassing, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f8353-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="f8353-110">U kunt een verbinding met extern bureaublad in uw rol tijdens het ontwikkelen van inschakelen door Hallo extern bureaublad-modules in de servicedefinitie van de of u kunt tooenable extern bureaublad via Hallo uitbreidingsmodule Extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="f8353-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="f8353-111">Hallo is gewenste aanpak toouse Hallo extern bureaublad-uitbreiding zoals u extern bureaublad inschakelen kunt, zelfs nadat de toepassing hello zonder tooredeploy uw toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f8353-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="f8353-112">Extern bureaublad configureren via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="f8353-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="f8353-113">Hello Azure-portal gebruikt Hallo uitbreidingsmodule Extern bureaublad-benadering, zodat u extern bureaublad inschakelen kunt, zelfs nadat het Hallo-toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f8353-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="f8353-114">Hallo **extern bureaublad** blade voor uw cloudservice, kunt u tooenable extern bureaublad, wijziging Hallo lokale Administrator-account gebruikt tooconnect toohello virtuele machines, Hallo certificaat gebruikt bij de verificatie en Hallo instellen de vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="f8353-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="f8353-115">Klik op **Cloudservices**Hallo-naam van de cloudservice Hallo op en klik vervolgens op **extern bureaublad**.</span><span class="sxs-lookup"><span data-stu-id="f8353-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="f8353-117">Kies of u tooenable extern bureaublad voor een afzonderlijke functie of voor alle functies wilt en Hallo-waarde van Hallo schakelbaar ook wijzigen**ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="f8353-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="f8353-118">Vul de velden Hallo vereist voor de gebruikersnaam, wachtwoord, verlopen en certificaat.</span><span class="sxs-lookup"><span data-stu-id="f8353-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="f8353-120">Alle exemplaren van de functie wordt opnieuw gestart wanneer u eerst Extern bureaublad inschakelen en klik op OK (vinkje).</span><span class="sxs-lookup"><span data-stu-id="f8353-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="f8353-121">tooprevent opnieuw worden opgestart, gebruikte tooencrypt Hallo-Hallo certificaatwachtwoord moet worden geïnstalleerd op Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="f8353-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="f8353-122">tooprevent opnieuw is opgestart, [upload een certificaat voor de cloudservice hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) en ga daarna terug toothis dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f8353-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="f8353-123">In **rollen**, selecteer Hallo rol of wilt u tooupdate Selecteer **alle** voor alle functies.</span><span class="sxs-lookup"><span data-stu-id="f8353-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="f8353-124">Wanneer u klaar bent met de updates voor uw configuratie, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8353-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="f8353-125">Het duurt enige tijd duren voordat uw rolinstanties gereed tooreceive verbindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="f8353-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="f8353-126">De afstand in rolinstanties</span><span class="sxs-lookup"><span data-stu-id="f8353-126">Remote into role instances</span></span>
<span data-ttu-id="f8353-127">Zodra de extern bureaublad op Hallo-functies is ingeschakeld, kunt u een verbinding rechtstreeks vanuit hello Azure-Portal te starten:</span><span class="sxs-lookup"><span data-stu-id="f8353-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="f8353-128">Klik op **exemplaren** tooopen hello **exemplaren** blade.</span><span class="sxs-lookup"><span data-stu-id="f8353-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="f8353-129">Selecteer een rolexemplaar met extern bureaublad die zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f8353-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="f8353-130">Klik op **Connect** toodownload een RDP-bestand voor de rolinstantie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8353-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="f8353-132">Klik op **Open** en vervolgens **Connect** toostart Hallo extern bureaublad-verbinding.</span><span class="sxs-lookup"><span data-stu-id="f8353-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="f8353-133">Als uw cloudservice zich bevindt achter een NSG, moet u mogelijk toocreate regels die verkeer op poorten toestaan **3389** en **20000**.</span><span class="sxs-lookup"><span data-stu-id="f8353-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="f8353-134">Extern bureaublad maakt gebruik van poort **3389**.</span><span class="sxs-lookup"><span data-stu-id="f8353-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="f8353-135">Cloud Service-exemplaren worden verdeeld, zodat u niet rechtstreeks welke tooconnect exemplaar om te controleren.</span><span class="sxs-lookup"><span data-stu-id="f8353-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="f8353-136">Hallo *RemoteForwarder* en *RemoteAccess* agents beheren van RDP-verkeer en Hallo client toosend een RDP-cookie toestaan en opgeven van een afzonderlijke instantie tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="f8353-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="f8353-137">Hallo *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000*** worden geopend die worden geblokkeerd als er een NSG.</span><span class="sxs-lookup"><span data-stu-id="f8353-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8353-138">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f8353-138">Additional resources</span></span>

<span data-ttu-id="f8353-139">[Hoe tooConfigure Cloudservices](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="f8353-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
