---
title: Inschakelen van extern bureaublad-Connection voor een rol in Azure-Cloudservices | Microsoft Docs
description: Het configureren van uw azure-cloud-servicetoepassing voor het toestaan van extern bureaublad-verbindingen
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="cad23-103">Verbinding met extern bureaublad voor een rol in Azure Cloudservices inschakelen</span><span class="sxs-lookup"><span data-stu-id="cad23-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cad23-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cad23-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="cad23-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cad23-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="cad23-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cad23-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="cad23-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cad23-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="cad23-108">Extern bureaublad kunt u toegang tot het bureaublad van een rol in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cad23-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="cad23-109">U kunt een verbinding met extern bureaublad gebruiken oplossen en analyseren van problemen met uw toepassing, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cad23-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="cad23-110">U kunt een verbinding met extern bureaublad in uw rol tijdens het ontwikkelen van inschakelen door de extern bureaublad-modules in de servicedefinitie van de of u kunt Extern bureaublad via de extern bureaublad-uitbreiding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cad23-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="cad23-111">De gewenste aanpak is het gebruik van de extern bureaublad-extensie, zoals u extern bureaublad inschakelen kunt, zelfs nadat de toepassing zonder opnieuw te implementeren van uw toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cad23-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="cad23-112">Extern bureaublad configureren via de Azure portal</span><span class="sxs-lookup"><span data-stu-id="cad23-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="cad23-113">De Azure-portal maakt gebruik van de aanpak van extern bureaublad-extensie zodat u extern bureaublad inschakelen kunt, zelfs nadat de toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cad23-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="cad23-114">De **extern bureaublad** blade voor uw cloudservice kunt u extern bureaublad inschakelen door het lokale Administrator-account gebruikt om verbinding met de virtuele machines te wijzigen, het certificaat in verificatie gebruikt en de verloopdatum instellen.</span><span class="sxs-lookup"><span data-stu-id="cad23-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="cad23-115">Klik op **Cloudservices**, klik op de naam van de cloudservice en klik vervolgens op **extern bureaublad**.</span><span class="sxs-lookup"><span data-stu-id="cad23-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="cad23-117">Kies of u wilt extern bureaublad inschakelen voor een afzonderlijke functie of voor alle rollen en klik vervolgens op de waarde van de schakelbaar naar **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="cad23-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="cad23-118">Vul de vereiste velden voor gebruikersnaam, wachtwoord, verlopen en certificaat.</span><span class="sxs-lookup"><span data-stu-id="cad23-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="cad23-120">Alle exemplaren van de functie wordt opnieuw gestart wanneer u eerst Extern bureaublad inschakelen en klik op OK (vinkje).</span><span class="sxs-lookup"><span data-stu-id="cad23-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="cad23-121">Als u wilt voorkomen dat de computer opnieuw is opgestart, moet het certificaat dat wordt gebruikt voor het versleutelen van het wachtwoord worden geïnstalleerd op de rol.</span><span class="sxs-lookup"><span data-stu-id="cad23-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="cad23-122">Om te voorkomen dat een herstart [upload een certificaat voor de cloudservice](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) en keer vervolgens terug naar dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cad23-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="cad23-123">In **rollen**, selecteer de rol die u wilt bijwerken of selecteer **alle** voor alle functies.</span><span class="sxs-lookup"><span data-stu-id="cad23-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="cad23-124">Wanneer u klaar bent met de updates voor uw configuratie, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cad23-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="cad23-125">Het duurt enige tijd duren voordat uw rolinstanties gereed zijn voor het ontvangen van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="cad23-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="cad23-126">De afstand in rolinstanties</span><span class="sxs-lookup"><span data-stu-id="cad23-126">Remote into role instances</span></span>
<span data-ttu-id="cad23-127">Zodra de extern bureaublad is ingeschakeld op de functies, kunt u een verbinding rechtstreeks vanuit de Azure-Portal te starten:</span><span class="sxs-lookup"><span data-stu-id="cad23-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="cad23-128">Klik op **exemplaren** openen de **exemplaren** blade.</span><span class="sxs-lookup"><span data-stu-id="cad23-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="cad23-129">Selecteer een rolexemplaar met extern bureaublad die zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cad23-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="cad23-130">Klik op **Connect** voor het downloaden van een RDP-bestand voor de rolinstantie.</span><span class="sxs-lookup"><span data-stu-id="cad23-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="cad23-132">Klik op **Open** en vervolgens **Connect** starten van de extern bureaublad-verbinding.</span><span class="sxs-lookup"><span data-stu-id="cad23-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="cad23-133">Als uw cloudservice zich bevindt achter een NSG, moet u mogelijk maken van regels die verkeer op poorten toestaan **3389** en **20000**.</span><span class="sxs-lookup"><span data-stu-id="cad23-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="cad23-134">Extern bureaublad maakt gebruik van poort **3389**.</span><span class="sxs-lookup"><span data-stu-id="cad23-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="cad23-135">Cloud Service-exemplaren worden verdeeld, zodat u direct welk exemplaar verbinding maken met kan niet bepalen.</span><span class="sxs-lookup"><span data-stu-id="cad23-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="cad23-136">De *RemoteForwarder* en *RemoteAccess* agents RDP-verkeer te beheren en dat de client verzenden van een cookie RDP en geeft u een afzonderlijk exemplaar verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="cad23-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="cad23-137">De *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000*** worden geopend die worden geblokkeerd als er een NSG.</span><span class="sxs-lookup"><span data-stu-id="cad23-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cad23-138">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cad23-138">Additional resources</span></span>

<span data-ttu-id="cad23-139">[Cloud-Services configureren hoe](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="cad23-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
