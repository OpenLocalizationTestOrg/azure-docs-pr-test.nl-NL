---
title: aaaConnect Windows-computers tooAzure Log Analytics | Microsoft Docs
description: Dit artikel ziet Hallo stappen tooconnect Hallo Windows-computers in uw lokale infrastructuur toohello Log Analytics-service met behulp van een aangepaste versie van Microsoft Monitoring Agent (MMA) Hallo.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="f7940-103">Verbinding maken met Windows-computers toohello Log Analytics-service in Azure</span><span class="sxs-lookup"><span data-stu-id="f7940-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="f7940-104">In dit artikel bevat de stappen Hallo tooconnect Windows-computers in uw lokale infrastructuur tooOMS werkruimten met behulp van een aangepaste versie van Microsoft Monitoring Agent (MMA) Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7940-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="f7940-105">U moet tooinstall en verbinding maken met agents voor alle Hallo computers die u wilt tooonboard zodat ze toosend data toohello Log Analytics-service en tooview en act van die gegevens.</span><span class="sxs-lookup"><span data-stu-id="f7940-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="f7940-106">Elke agent kan toomultiple werkruimten rapporteren.</span><span class="sxs-lookup"><span data-stu-id="f7940-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="f7940-107">U kunt met behulp van de installatie vanaf de opdrachtregel, agents installeren of met Desired State Configuration (DSC) in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f7940-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="f7940-108">Voor virtuele machines in Azure wordt uitgevoerd, kunt u de installatie vereenvoudigen met behulp van Hallo [extensie van virtuele machine](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f7940-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="f7940-109">Hallo-agent gebruikt op computers met een internetverbinding, Hallo verbinding toohello Internet toosend gegevens tooOMS.</span><span class="sxs-lookup"><span data-stu-id="f7940-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="f7940-110">Voor computers die u geen verbinding met Internet hebt, kunt u een proxy of Hallo [OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f7940-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="f7940-111">Verbinding maken met uw Windows-computers tooOMS is eenvoudig met behulp van de drie eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="f7940-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="f7940-112">Hallo agent setup-bestand downloaden van Hallo OMS-portal</span><span class="sxs-lookup"><span data-stu-id="f7940-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="f7940-113">Hallo agent installeren met Hallo methode die u kiest</span><span class="sxs-lookup"><span data-stu-id="f7940-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="f7940-114">Hallo-agent configureren of het toevoegen van extra werkruimten, indien nodig</span><span class="sxs-lookup"><span data-stu-id="f7940-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="f7940-115">Hallo volgende diagram toont Hallo relatie tussen uw Windows-computers en OMS nadat u hebt geïnstalleerd en geconfigureerd agents.</span><span class="sxs-lookup"><span data-stu-id="f7940-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![OMS-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="f7940-117">Als de beleidsregels van uw IT-beveiliging niet toestaan computers op uw netwerk tooconnect toohello Internet dat, kunt u uw computers tooconnect toohello OMS-Gateway configureren.</span><span class="sxs-lookup"><span data-stu-id="f7940-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="f7940-118">Voor meer informatie en stapsgewijze instructies voor hoe tooconfigure uw toocommunicate servers via een OMS-Gateway toohello OMS-service, bekijken [verbinding maken met computers tooOMS Hallo OMS-Gateway met](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f7940-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="f7940-119">Systeemvereisten en de vereiste configuratie</span><span class="sxs-lookup"><span data-stu-id="f7940-119">System requirements and required configuration</span></span>
<span data-ttu-id="f7940-120">Voordat u installeert of agents te implementeren, controleert u Hallo details tooensure u voldoet aan de vereisten hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="f7940-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="f7940-121">U kunt alleen Hallo OMS MMA installeren op computers met Windows Server 2008 SP 1 of hoger of Windows 7 SP1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f7940-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="f7940-122">U moet een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f7940-122">You need an Azure subscription.</span></span>  <span data-ttu-id="f7940-123">Zie voor meer informatie [aan de slag met logboekanalyse](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f7940-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="f7940-124">Elke computer met Windows moet kunnen tooconnect toohello Internet met behulp van HTTPS- of toohello OMS-Gateway.</span><span class="sxs-lookup"><span data-stu-id="f7940-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="f7940-125">Deze verbinding kan worden direct, via een proxy of via Hallo OMS-Gateway.</span><span class="sxs-lookup"><span data-stu-id="f7940-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="f7940-126">U kunt Hallo OMS MMA installeren op zelfstandige computers, servers en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f7940-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="f7940-127">Als u tooconnect Azure gehoste virtuele machines tooOMS wilt, Zie [verbinding maken met Azure virtuele machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f7940-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="f7940-128">Hallo-agent moet toouse TCP-poort 443 voor verschillende bronnen.</span><span class="sxs-lookup"><span data-stu-id="f7940-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="f7940-129">Netwerk</span><span class="sxs-lookup"><span data-stu-id="f7940-129">Network</span></span>

<span data-ttu-id="f7940-130">Voor Windows-agents tooconnect tooand registreren met Hallo OMS-service, moeten ze toegang toonetwork bronnen, met inbegrip van poortnummers Hallo en domein-URL's hebben.</span><span class="sxs-lookup"><span data-stu-id="f7940-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="f7940-131">Proxy-servers moet u tooensure die Hallo juiste proxyserver resources zijn geconfigureerd in instellingen voor de agent.</span><span class="sxs-lookup"><span data-stu-id="f7940-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="f7940-132">Voor firewalls die toegang toohello Internet beperken, moeten u of uw netwerken engineers tooconfigure uw firewall toopermit toegang tooOMS.</span><span class="sxs-lookup"><span data-stu-id="f7940-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="f7940-133">De agent-instellingen hoeven niet te worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="f7940-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="f7940-134">Hallo volgende tabel ziet u bronnen die nodig zijn voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="f7940-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="f7940-135">Aantal Hallo na bronnen vermeld operationeel inzicht, waarop een vorige naam op voor logboekanalyse is.</span><span class="sxs-lookup"><span data-stu-id="f7940-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="f7940-136">Agentresource</span><span class="sxs-lookup"><span data-stu-id="f7940-136">Agent Resource</span></span> | <span data-ttu-id="f7940-137">Poorten</span><span class="sxs-lookup"><span data-stu-id="f7940-137">Ports</span></span> | <span data-ttu-id="f7940-138">HTTPS-controle overslaan</span><span class="sxs-lookup"><span data-stu-id="f7940-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="f7940-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f7940-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="f7940-140">443</span><span class="sxs-lookup"><span data-stu-id="f7940-140">443</span></span> | <span data-ttu-id="f7940-141">Ja</span><span class="sxs-lookup"><span data-stu-id="f7940-141">Yes</span></span> |
| <span data-ttu-id="f7940-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f7940-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="f7940-143">443</span><span class="sxs-lookup"><span data-stu-id="f7940-143">443</span></span> | <span data-ttu-id="f7940-144">Ja</span><span class="sxs-lookup"><span data-stu-id="f7940-144">Yes</span></span> |
| <span data-ttu-id="f7940-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f7940-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="f7940-146">443</span><span class="sxs-lookup"><span data-stu-id="f7940-146">443</span></span> | <span data-ttu-id="f7940-147">Ja</span><span class="sxs-lookup"><span data-stu-id="f7940-147">Yes</span></span> |
| <span data-ttu-id="f7940-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="f7940-148">*.azure-automation.net</span></span> | <span data-ttu-id="f7940-149">443</span><span class="sxs-lookup"><span data-stu-id="f7940-149">443</span></span> | <span data-ttu-id="f7940-150">Ja</span><span class="sxs-lookup"><span data-stu-id="f7940-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="f7940-151">Hallo agent setup-bestand downloaden van OMS</span><span class="sxs-lookup"><span data-stu-id="f7940-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="f7940-152">In Hallo OMS-portal op Hallo **overzicht** pagina, klikt u op Hallo **instellingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="f7940-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="f7940-153">Klik op Hallo **verbonden bronnen** Hallo boven op tabblad.</span><span class="sxs-lookup"><span data-stu-id="f7940-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="f7940-154">![Tabblad verbonden bronnen](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="f7940-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="f7940-155">Klik op **Windows-Servers** en klik vervolgens op **Windows-Agent downloaden** toepasselijke tooyour computer processor type toodownload Hallo setup-bestand.</span><span class="sxs-lookup"><span data-stu-id="f7940-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="f7940-156">Op Hallo van **werkruimte-ID**en klik op de pictogram kopiëren Hallo Hallo-ID in Kladblok plakken.</span><span class="sxs-lookup"><span data-stu-id="f7940-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="f7940-157">Op Hallo van **primaire sleutel**, klik op de pictogram kopiëren Hallo en Hallo-sleutel in Kladblok plakken.</span><span class="sxs-lookup"><span data-stu-id="f7940-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="f7940-158">Hallo agent installeren met setup</span><span class="sxs-lookup"><span data-stu-id="f7940-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="f7940-159">Setup tooinstall Hallo agent uitvoeren op een computer die u toomanage wilt.</span><span class="sxs-lookup"><span data-stu-id="f7940-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="f7940-160">Klik op de welkomstpagina Hallo **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7940-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="f7940-161">Lees de licentiebepalingen Hallo op de pagina licentievoorwaarden hello, en klik vervolgens op **ik ga akkoord**.</span><span class="sxs-lookup"><span data-stu-id="f7940-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="f7940-162">Op Hallo doelmap pagina wijzigen of de standaardinstallatiemap Hallo houden en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7940-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="f7940-163">Op Hallo installatieopties voor Agent pagina tooconnect Hallo agent tooAzure logboekanalyse (OMS), Operations Manager, kunt u of u kunt Hallo keuzes leeg laten als u wilt dat tooconfigure Hallo agent later.</span><span class="sxs-lookup"><span data-stu-id="f7940-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="f7940-164">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7940-164">Click **Next**.</span></span>   
    - <span data-ttu-id="f7940-165">Als u kiest tooconnect tooAzure logboekanalyse (OMS), plak Hallo **werkruimte-ID** en **Werkruimtesleutel (primaire sleutel)** die u in de vorige procedure Hallo in Kladblok hebt gekopieerd en klik vervolgens op  **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7940-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="f7940-166">![Werkruimte-ID en Primary Key plakken](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="f7940-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="f7940-167">Als u tooconnect tooOperations Manager hebt gekozen, typt u Hallo **Beheergroepsnaam**, **beheerserver** naam, en **Beheerserverpoort**, en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7940-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="f7940-168">Kies op Hallo Agentactieacount pagina Hallo lokale systeemaccount of een lokale account en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7940-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="f7940-169">![beheergroepconfiguratie](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![actie-account van agent](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="f7940-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="f7940-170">Controleer uw selecties op Hallo gereed tooInstall pagina en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="f7940-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="f7940-171">Pagina op Hallo configuratie is voltooid, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f7940-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="f7940-172">Als u klaar Hallo **Microsoft Monitoring Agent** wordt weergegeven in **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="f7940-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="f7940-173">U kunt uw configuratie er bekijken en controleren dat die Hallo-agent is verbonden tooOperational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="f7940-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="f7940-174">Wanneer verbonden tooOMS Hallo agent wordt een bericht weergegeven: **Hallo Microsoft Monitoring Agent verbonden is toohello Microsoft Operations Management Suite-service.**</span><span class="sxs-lookup"><span data-stu-id="f7940-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="f7940-175">Proxy-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="f7940-175">Configure proxy settings</span></span>

<span data-ttu-id="f7940-176">U kunt volgen procedure tooconfigure proxy-instellingen voor Microsoft Monitoring Agent via het Configuratiescherm Hallo Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f7940-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="f7940-177">U moet deze procedure toouse voor elke server.</span><span class="sxs-lookup"><span data-stu-id="f7940-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="f7940-178">Als u een groot aantal servers dat u tooconfigure nodig hebt, vindt u het misschien gemakkelijker toouse een script tooautomate dit proces.</span><span class="sxs-lookup"><span data-stu-id="f7940-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="f7940-179">Als dit het geval is, raadpleegt u de volgende procedure Hallo [tooconfigure proxy-instellingen voor Microsoft Monitoring Agent met een script Hallo](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="f7940-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="f7940-180">tooconfigure proxy-instellingen voor Hallo Microsoft Monitoring Agent via het Configuratiescherm</span><span class="sxs-lookup"><span data-stu-id="f7940-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="f7940-181">Open het **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="f7940-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="f7940-182">Open **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="f7940-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="f7940-183">Klik op Hallo **Proxy-instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f7940-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="f7940-184">![tabblad proxyinstellingen](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="f7940-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="f7940-185">Selecteer **een proxyserver gebruiken** en typ Hallo-URL en het poortnummer, indien nodig, vergelijkbaar toohello voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f7940-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="f7940-186">Als de proxyserver verificatie vereist, typt u Hallo gebruikersnaam en wachtwoord tooaccess Hallo proxyserver.</span><span class="sxs-lookup"><span data-stu-id="f7940-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="f7940-187">Controleer of de agent-connectiviteit tooOMS</span><span class="sxs-lookup"><span data-stu-id="f7940-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="f7940-188">U kunt eenvoudig controleren of uw agents communiceert Hallo procedure te volgen met OMS:</span><span class="sxs-lookup"><span data-stu-id="f7940-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="f7940-189">Open het Configuratiescherm op Hallo-computer met Windows-agent Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7940-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="f7940-190">Open Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="f7940-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="f7940-191">Klik op tabblad van hello Azure logboekanalyse (OMS).</span><span class="sxs-lookup"><span data-stu-id="f7940-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="f7940-192">U ziet in de kolom Status Hallo dat die Hallo-agent is verbonden met succes toohello Operations Management Suite-service.</span><span class="sxs-lookup"><span data-stu-id="f7940-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![Agent verbonden](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="f7940-194">tooconfigure proxy-instellingen voor Hallo Microsoft Monitoring Agent met een script</span><span class="sxs-lookup"><span data-stu-id="f7940-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="f7940-195">Kopieer Hallo volgende steekproef, bijwerken met specifieke tooyour omgeving, sla het bestand met extensie PS1 en vervolgens Hallo-script uitvoeren op elke computer die verbinding rechtstreeks toohello OMS-service maakt.</span><span class="sxs-lookup"><span data-stu-id="f7940-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="f7940-196">Hallo agent installeren met Hallo vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="f7940-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="f7940-197">Wijzigen en gebruik vervolgens Hallo voorbeeld tooinstall Hallo agent via de opdrachtregel hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="f7940-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="f7940-198">Hallo-voorbeeld wordt een volledig stille installatie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7940-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="f7940-199">Als u een agent tooupgrade wilt, moet u toouse Hallo logboekanalyse scripting API.</span><span class="sxs-lookup"><span data-stu-id="f7940-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="f7940-200">Zie Hallo volgende sectie tooupgrade een agent.</span><span class="sxs-lookup"><span data-stu-id="f7940-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="f7940-201">Hallo agent IExpress gebruikt als de zelfstandig uitpakken met Hallo `/c` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7940-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="f7940-202">U kunt opdrachtregelopties op Hallo zien [opdrachtregelopties voor IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) en vervolgens update Hallo voorbeeld toosuit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="f7940-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="f7940-203">MMA-specifieke opties</span><span class="sxs-lookup"><span data-stu-id="f7940-203">MMA-specific options</span></span>                   |<span data-ttu-id="f7940-204">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f7940-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="f7940-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="f7940-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="f7940-206">1 = configureren Hallo agent tooreport tooa werkruimte</span><span class="sxs-lookup"><span data-stu-id="f7940-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="f7940-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="f7940-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="f7940-208">Werkruimte-Id (guid) voor Hallo werkruimte tooadd</span><span class="sxs-lookup"><span data-stu-id="f7940-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="f7940-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="f7940-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="f7940-210">Werkruimte sleutel gebruikte tooinitially verifiëren met Hallo-werkruimte</span><span class="sxs-lookup"><span data-stu-id="f7940-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="f7940-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="f7940-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="f7940-212">Geef Hallo cloud-omgeving waar Hallo werkruimte zich bevindt</span><span class="sxs-lookup"><span data-stu-id="f7940-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="f7940-213">0 = azure commerciële cloudservice (standaard)</span><span class="sxs-lookup"><span data-stu-id="f7940-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="f7940-214">1 = azure Government</span><span class="sxs-lookup"><span data-stu-id="f7940-214">1 = Azure Government</span></span> |
|<span data-ttu-id="f7940-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="f7940-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="f7940-216">URI voor Hallo proxy toouse</span><span class="sxs-lookup"><span data-stu-id="f7940-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="f7940-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="f7940-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="f7940-218">Gebruikersnaam tooaccess een geverifieerde proxyserver</span><span class="sxs-lookup"><span data-stu-id="f7940-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="f7940-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="f7940-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="f7940-220">Wachtwoord tooaccess een geverifieerde proxyserver</span><span class="sxs-lookup"><span data-stu-id="f7940-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="f7940-221">tooavoid roept Hallo opdrachtregelprogramma lengtelimiet van IExpress, Hallo-agent installeren met geen werkruimte geconfigureerd en gebruik vervolgens de configuratie van een script tooset voor Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="f7940-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="f7940-222">Als u krijgt een `Command line option syntax error.` bij gebruik van Hallo `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, kunt u Hallo volgende tijdelijke oplossing:</span><span class="sxs-lookup"><span data-stu-id="f7940-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="f7940-223">Een werkruimte met een script toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7940-223">Add a workspace using a script</span></span>
<span data-ttu-id="f7940-224">Toevoegen van een werkruimte Hallo logboekanalyse agent scripting API gebruiken met Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7940-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="f7940-225">tooadd een werkruimte in Azure voor US Government, gebruik Hallo voorbeeldscript te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7940-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="f7940-226">Als u hebt gebruikt Hallo vanaf de opdrachtregel of eerder tooinstall script of Hallo-agent configureren `EnableAzureOperationalInsights` is vervangen door `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="f7940-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="f7940-227">Hallo agent installeren met DSC in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f7940-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="f7940-228">U kunt Hallo script voorbeeld tooinstall Hallo agent met behulp van DSC in Azure Automation te volgen.</span><span class="sxs-lookup"><span data-stu-id="f7940-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="f7940-229">Hallo-voorbeeld installeert de 64-bits agent, geïdentificeerd door Hallo Hallo `URI` waarde.</span><span class="sxs-lookup"><span data-stu-id="f7940-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="f7940-230">U kunt ook Hallo 32-bits versie door te vervangen Hallo URI-waarde.</span><span class="sxs-lookup"><span data-stu-id="f7940-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="f7940-231">Hallo URI's voor beide versies zijn:</span><span class="sxs-lookup"><span data-stu-id="f7940-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="f7940-232">Windows 64-bits agent - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="f7940-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="f7940-233">Windows 32-bits agent - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="f7940-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="f7940-234">In dit voorbeeld procedure en het script wordt een bestaand agent niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f7940-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="f7940-235">Hallo xPSDesiredStateConfiguration DSC-Module importeren uit [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f7940-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="f7940-236">Maken van Azure Automation-variabele assets voor *OPSINSIGHTS_WS_ID* en *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="f7940-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="f7940-237">Stel *OPSINSIGHTS_WS_ID* tooyour logboekanalyse OMS-werkruimte-ID en stel *OPSINSIGHTS_WS_KEY* toohello primaire sleutel van uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="f7940-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="f7940-238">Hallo volgende script en sla deze op als MMAgent.ps1 gebruiken</span><span class="sxs-lookup"><span data-stu-id="f7940-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="f7940-239">Wijzigen en gebruik vervolgens Hallo voorbeeld tooinstall Hallo agent met behulp van DSC in Azure Automation te volgen.</span><span class="sxs-lookup"><span data-stu-id="f7940-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="f7940-240">MMAgent.ps1 in Azure Automation importeren met behulp van hello Azure Automation-interface of de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f7940-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="f7940-241">De configuratie van een knooppunt toohello toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f7940-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="f7940-242">Hallo knooppunt controleert de configuratie en Hallo MMA wordt doorgeschoven, toohello knooppunt binnen 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="f7940-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="f7940-243">Hallo laatste ProductId waarde ophalen</span><span class="sxs-lookup"><span data-stu-id="f7940-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="f7940-244">Hallo `ProductId value` in Hallo MMAgent.ps1 script unieke tooeach agent-versie is.</span><span class="sxs-lookup"><span data-stu-id="f7940-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="f7940-245">Wanneer een bijgewerkte versie van elke agent wordt gepubliceerd, verandert de Hallo-product-id-waarde.</span><span class="sxs-lookup"><span data-stu-id="f7940-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="f7940-246">Wanneer Hallo ProductId wordt gewijzigd in toekomstige hello, kunt u dus Hallo agent-versie met een eenvoudige script vinden.</span><span class="sxs-lookup"><span data-stu-id="f7940-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="f7940-247">Nadat u Hallo nieuwste agentversie is geïnstalleerd op een testserver hebt, kunt u Hallo Scriptwaarde tooget hello geïnstalleerd ProductId te volgen.</span><span class="sxs-lookup"><span data-stu-id="f7940-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="f7940-248">Hallo laatste ProductId waarde kunt u Hallo-waarde in Hallo MMAgent.ps1 script bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f7940-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="f7940-249">Een agent handmatig configureren of extra werkruimten toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7940-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="f7940-250">Als u agents hebt geïnstalleerd, maar kon niet configureren of als u wilt dat Hallo agent tooreport toomultiple werkruimten, kunt u deze kunt gebruiken Hallo informatie tooenable een agent te volgen of configureer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f7940-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="f7940-251">Nadat u de agent Hallo hebt geconfigureerd, worden geregistreerd bij Hallo agent-service en krijgen de vereiste configuratiegegevens en management packs die oplossingsgegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="f7940-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="f7940-252">Nadat u Hallo Microsoft Monitoring Agent hebt geïnstalleerd, opent u **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="f7940-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="f7940-253">Open **Microsoft Monitoring Agent** en klik vervolgens op Hallo **Azure logboekanalyse (OMS)** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f7940-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="f7940-254">Klik op **toevoegen** tooopen hello **Log Analytics-werkruimte toevoegen** vak.</span><span class="sxs-lookup"><span data-stu-id="f7940-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="f7940-255">Plakken Hallo **werkruimte-ID** en **Werkruimtesleutel (primaire sleutel)** dat u hebt gekopieerd in Kladblok in een eerdere procedure voor Hallo werkruimte wilt tooadd uit te voeren en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7940-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="f7940-256">![Configureer operationeel inzicht](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="f7940-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="f7940-257">Nadat gegevens worden verzameld van computers die worden bewaakt door Hallo-agent, het aantal computers worden bewaakt door OMS Hallo verschijnen in Hallo OMS-portal op Hallo **verbonden bronnen** tabblad **instellingen** als  **Servers die zijn verbonden**.</span><span class="sxs-lookup"><span data-stu-id="f7940-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="f7940-258">toodisable een agent</span><span class="sxs-lookup"><span data-stu-id="f7940-258">toodisable an agent</span></span>
1. <span data-ttu-id="f7940-259">Open na de installatie van agent Hallo **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="f7940-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="f7940-260">Microsoft Monitoring Agent te openen en klik vervolgens op Hallo **Azure logboekanalyse (OMS)** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f7940-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="f7940-261">Selecteer een werkruimte en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="f7940-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="f7940-262">Herhaal deze stap voor alle andere werkruimten.</span><span class="sxs-lookup"><span data-stu-id="f7940-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="f7940-263">Configureer desgewenst agents tooreport tooan Operations Manager-beheergroep</span><span class="sxs-lookup"><span data-stu-id="f7940-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="f7940-264">Als u Operations Manager in uw IT-infrastructuur, kunt u ook Hallo MMA agent gebruiken als een Operations Manager-agent.</span><span class="sxs-lookup"><span data-stu-id="f7940-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="f7940-265">tooconfigure MMA agents tooreport tooan Operations Manager-beheergroep</span><span class="sxs-lookup"><span data-stu-id="f7940-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="f7940-266">Open op Hallo-computer waarop Hallo-agent is geïnstalleerd, **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="f7940-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="f7940-267">Open **Microsoft Monitoring Agent** en klik vervolgens op Hallo **Operations Manager** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f7940-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="f7940-268">![Microsoft Monitoring Agent Operations Manager-tabblad](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="f7940-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="f7940-269">Als uw Operations Manager-servers integratie met Active Directory hebt, klikt u op **automatisch bijwerken van beheergroeptoewijzingen van AD DS**.</span><span class="sxs-lookup"><span data-stu-id="f7940-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="f7940-270">Klik op **toevoegen** tooopen hello **toevoegen van een beheergroep** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7940-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="f7940-271">![Microsoft Monitoring Agent een beheergroep toevoegen](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="f7940-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="f7940-272">In **beheergroepsnaam** vak, type Hallo-naam van uw beheergroep.</span><span class="sxs-lookup"><span data-stu-id="f7940-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="f7940-273">In Hallo **primaire beheerserver** vak, typ de computernaam van de primaire beheerserver Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7940-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="f7940-274">In Hallo **beheerserverpoort** vak type Hallo TCP-poortnummer.</span><span class="sxs-lookup"><span data-stu-id="f7940-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="f7940-275">Onder **Agentactieacount**, kies Hallo lokale systeemaccount of een lokale account.</span><span class="sxs-lookup"><span data-stu-id="f7940-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="f7940-276">Klik op **OK** tooclose hello **toevoegen van een beheergroep** in het dialoogvenster en klik vervolgens op **OK** tooclose hello **Microsoft Monitoring Agenteigenschappen**in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7940-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7940-277">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7940-277">Next steps</span></span>

- <span data-ttu-id="f7940-278">[Log Analytics-oplossingen van Hallo oplossingen galerie toevoegen](log-analytics-add-solutions.md) tooadd functionaliteit en verzamelen gegevens.</span><span class="sxs-lookup"><span data-stu-id="f7940-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
