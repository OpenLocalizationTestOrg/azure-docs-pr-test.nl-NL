---
title: aaa"Azure VM waarschuwingen met Automation-Runbooks oplossen | Microsoft Docs'
description: In dit artikel laat zien hoe toointegrate virtuele Machine van Azure met Azure Automation-runbooks waarschuwingen en automatisch oplossen van problemen
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="0e975-103">Azure Automation-scenario: waarschuwingen van de virtuele machine in Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="0e975-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="0e975-104">Azure Automation en Azure Virtual Machines hebben een nieuwe functie waarmee u tooconfigure virtuele Machine (VM) waarschuwingen toorun Automation-runbooks uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="0e975-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="0e975-105">Deze nieuwe mogelijkheid kunt u tooautomatically uit te voeren standaard in het antwoord tooVM waarschuwingen, zoals opnieuw te starten of stoppen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="0e975-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="0e975-106">Voorheen tijdens het maken van de waarschuwingsregel VM kon u te[opgeven van een Automation-webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in de volgorde toorun hello runbook wanneer Hallo waarschuwing geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0e975-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="0e975-107">Maar vereist dit dat u toodo Hallo werk van Hallo runbook maken, Hallo webhook voor Hallo-runbook maken en vervolgens te kopiëren en plakken Hallo webhook tijdens het maken van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="0e975-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="0e975-108">Met deze nieuwe versie is Hallo-proces is veel eenvoudiger omdat u een runbook rechtstreeks uit een lijst tijdens het maken van de waarschuwingsregel kiezen kunt en kunt u een automatiseringsaccount dat wordt Hallo runbook uitvoeren of een account gemakkelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="0e975-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="0e975-109">In dit artikel wordt ziet u hoe eenvoudig het is tooset van een virtuele machine van Azure-waarschuwing en een Automation-runbook-toorun configureren wanneer Hallo waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0e975-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="0e975-110">Voorbeeldscenario's bevatten een virtuele machine opnieuw te starten wanneer het geheugengebruik Hallo sommige vanwege tooan toepassing op Hallo VM met een geheugenlek overschrijdt of een virtuele machine stoppen wanneer Hallo CPU Gebruikerstijd minder dan 1% voor het afgelopen uur is en niet gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="0e975-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="0e975-111">Ook wordt uitgelegd hoe Hallo automatisch maken van een service-principal in uw Automation-account vereenvoudigt Hallo gebruik van runbooks in Azure waarschuwing herbemiddeling.</span><span class="sxs-lookup"><span data-stu-id="0e975-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="0e975-112">Een waarschuwing op een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="0e975-112">Create an alert on a VM</span></span>
<span data-ttu-id="0e975-113">Voer Hallo volgende stappen tooconfigure een waarschuwing toolaunch een runbook wanneer de drempel is voldaan.</span><span class="sxs-lookup"><span data-stu-id="0e975-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="0e975-114">Met deze release alleen wordt ondersteund V2 virtuele machines en ondersteuning voor klassieke die virtuele machines wordt binnenkort toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0e975-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="0e975-115">Meld u bij toohello Azure-portal en klikt u op **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="0e975-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="0e975-116">Selecteer een van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0e975-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="0e975-117">Hallo virtuele machine dashboard blade worden weergegeven en Hallo **instellingen** blade tooits rechts.</span><span class="sxs-lookup"><span data-stu-id="0e975-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="0e975-118">Van Hallo **instellingen** blade onder Hallo bewaking sectie Selecteer **waarschuwing regels**.</span><span class="sxs-lookup"><span data-stu-id="0e975-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="0e975-119">Op Hallo **waarschuwing regels** blade, klikt u op **waarschuwing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0e975-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="0e975-120">Hiermee opent u up Hallo **een waarschuwingsregel toevoegen** blade kunt u voorwaarden voor de waarschuwing Hallo Hallo configureren en kiezen uit een of meer van deze opties: toosomeone e-mailbericht verzenden, gebruikt u een systeem webhook tooforward Hallo waarschuwing tooanother en/of een Automation-runbook worden uitgevoerd in reactie poging tooremediate Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="0e975-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="0e975-121">Een runbook configureren</span><span class="sxs-lookup"><span data-stu-id="0e975-121">Configure a runbook</span></span>
<span data-ttu-id="0e975-122">tooconfigure een runbook toorun als Hallo VM waarschuwingsdrempel wordt voldaan, selecteer **Automation-Runbook**.</span><span class="sxs-lookup"><span data-stu-id="0e975-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="0e975-123">In Hallo **runbook configureren** blade kunt u Hallo runbook toorun en Hallo Automation-account toorun hello runbook in.</span><span class="sxs-lookup"><span data-stu-id="0e975-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Configureer een Automation-runbook en een nieuw Automation-Account maken](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="0e975-125">Voor deze release kunt u kiezen uit drie runbooks waarmee Hallo service – VM starten, stoppen VM of VM verwijderen (verwijderen).</span><span class="sxs-lookup"><span data-stu-id="0e975-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="0e975-126">Hallo mogelijkheid tooselect andere runbooks of een van uw eigen runbooks in een toekomstige release beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="0e975-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Toochoose van Runbooks](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="0e975-128">Nadat u een Hallo drie beschikbare runbooks selecteert, Hallo **Automation-account** vervolgkeuzelijst wordt weergegeven en kunt u een automation account Hallo runbook wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e975-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="0e975-129">Runbooks moeten toorun in Hallo context van een [Automation-account](automation-security-overview.md) die zich in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0e975-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="0e975-130">U kunt een Automation-account dat u al hebt gemaakt, of u kunt een nieuw Automation-account voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0e975-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="0e975-131">Hallo runbooks die worden geleverd verifiëren met een service-principal tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0e975-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="0e975-132">Als u toorun hello runbook in een van uw bestaande Automation-accounts kiest, wordt automatisch gemaakt Hallo service principal voor u.</span><span class="sxs-lookup"><span data-stu-id="0e975-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="0e975-133">Als u toocreate een nieuw automatiseringsaccount kiest, wordt klikt u vervolgens we automatisch gemaakt Hallo-account en Hallo service-principal.</span><span class="sxs-lookup"><span data-stu-id="0e975-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="0e975-134">In beide gevallen twee activa ook worden gemaakt in Hallo Automation-account de activa van een certificaat met de naam **AzureRunAsCertificate** en de activa van een verbinding met de naam **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="0e975-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="0e975-135">Hallo runbooks gebruikt **AzureRunAsConnection** tooauthenticate met Azure in volgorde tooperform Hallo management actie tegen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="0e975-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="0e975-136">Hallo service-principal in Hallo abonnementsbereik wordt gemaakt en rol van Inzender Hallo is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0e975-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="0e975-137">Deze rol is vereist om Hallo account toohave machtiging toorun Automation-runbooks toomanage virtuele Azure-machines.</span><span class="sxs-lookup"><span data-stu-id="0e975-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="0e975-138">Hallo maken van een account Automaton en/of de service-principal is een eenmalige gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="0e975-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="0e975-139">Zodra ze zijn gemaakt, kunt u dat account toorun runbooks voor andere virtuele machine van Azure-waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="0e975-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="0e975-140">Wanneer u klikt op **OK** Hallo waarschuwing is geconfigureerd en als u Hallo optie toocreate een nieuw automatiseringsaccount hebt geselecteerd, samen met de service-principal hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0e975-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="0e975-141">Dit kan enkele seconden duren toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0e975-141">This can take a few seconds toocomplete.</span></span>  

![Runbook wordt geconfigureerd](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="0e975-143">Nadat Hallo-configuratie is voltooid, ziet u Hallo de naam van Hallo runbook weergeven in Hallo **een waarschuwingsregel toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="0e975-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Runbook is geconfigureerd](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="0e975-145">Klik op **OK** in Hallo **een waarschuwingsregel toevoegen** blade en Hallo waarschuwingsregel wordt gemaakt en wordt geactiveerd als Hallo virtuele machine actief is.</span><span class="sxs-lookup"><span data-stu-id="0e975-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="0e975-146">In- of uitschakelen van een runbook</span><span class="sxs-lookup"><span data-stu-id="0e975-146">Enable or disable a runbook</span></span>
<span data-ttu-id="0e975-147">Als u een runbook dat is geconfigureerd voor een waarschuwing hebt, kunt u deze uitschakelen zonder te verwijderen van de runbookconfiguratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0e975-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="0e975-148">Dit kunt u tookeep Hallo waarschuwing uitgevoerd en sommige Hallo waarschuwingsregels mogelijk te testen en later opnieuw inschakelen Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="0e975-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="0e975-149">Een runbook maken dat met een Azure-waarschuwing werkt</span><span class="sxs-lookup"><span data-stu-id="0e975-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="0e975-150">Wanneer u een runbook als onderdeel van een Azure waarschuwingsregel kiest, moet Hallo runbook toohave logica in het toomanage Hallo waarschuwingsgegevens die tooit wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="0e975-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="0e975-151">Wanneer een runbook is geconfigureerd in een waarschuwingsregel, is een webhook gemaakt voor runbook Hallo; Deze webhook is en gebruikte toostart Hallo runbook elke waarschuwing tijd Hallo-triggers.</span><span class="sxs-lookup"><span data-stu-id="0e975-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="0e975-152">Hallo werkelijke aanroep toostart hello runbook is een HTTP POST-aanvraag toohello webhook-URL.</span><span class="sxs-lookup"><span data-stu-id="0e975-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="0e975-153">Hallo-hoofdtekst van Hallo POST-aanvraag bevat een JSON-indeling object dat nuttige eigenschappen gerelateerde toohello waarschuwing bevat.</span><span class="sxs-lookup"><span data-stu-id="0e975-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="0e975-154">Zoals u hieronder zien kunt, bevat de waarschuwingsgegevens Hallo-gegevens, zoals de abonnements-id, resourceGroupName resourceName en resourceType.</span><span class="sxs-lookup"><span data-stu-id="0e975-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="0e975-155">Voorbeeld van waarschuwingsgegevens</span><span class="sxs-lookup"><span data-stu-id="0e975-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="0e975-156">Wanneer Hallo Automation-webhook-service Hallo HTTP POST ontvangt Hallo waarschuwingsgegevens extraheert en geeft deze door toohello runbook in runbookinvoerparameter WebhookData Hallo.</span><span class="sxs-lookup"><span data-stu-id="0e975-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="0e975-157">Hieronder vindt u een voorbeeldrunbook dat toont hoe toouse Hallo WebhookData-parameter en waarschuwingsgegevens Hallo uitpakken en toomanage hello Azure-resource die Hallo waarschuwing heeft geactiveerd worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0e975-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="0e975-158">Voorbeeldrunbook</span><span class="sxs-lookup"><span data-stu-id="0e975-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="0e975-159">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="0e975-159">Summary</span></span>
<span data-ttu-id="0e975-160">Wanneer u een waarschuwing op een virtuele machine in Azure configureert, hebt u nu Hallo mogelijkheid tooeasily configureren van een Automation runbook tooautomatically herstelactie uitvoeren wanneer het Hallo-waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0e975-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="0e975-161">Voor deze release kunt u kiezen uit runbooks toorestart, stoppen of verwijderen van een virtuele machine, afhankelijk van uw waarschuwing scenario.</span><span class="sxs-lookup"><span data-stu-id="0e975-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="0e975-162">Dit is alleen Hallo begin van het inschakelen van scenario's waarbij u Hallo acties (melding, het oplossen van problemen herstel) die automatisch worden uitgevoerd wanneer een waarschuwing activeert beheren.</span><span class="sxs-lookup"><span data-stu-id="0e975-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e975-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e975-163">Next Steps</span></span>
* <span data-ttu-id="0e975-164">Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="0e975-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="0e975-165">tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="0e975-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="0e975-166">toolearn meer informatie over runbooktypen, hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="0e975-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

