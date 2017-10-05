---
title: " Herstellen van de Azure VM waarschuwingen met Automation-Runbooks | Microsoft Docs"
description: Dit artikel wordt beschreven hoe u waarschuwingen van de virtuele Machine van Azure integreren met Azure Automation-runbooks en automatisch oplossen van problemen
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
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="49cd9-103">Azure Automation-scenario: waarschuwingen van de virtuele machine in Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="49cd9-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="49cd9-104">Azure Automation en Azure Virtual Machines zijn beschikbaar voor een nieuwe functie waarmee u kunt de virtuele Machine (VM) waarschuwingen configureren om te Automation-runbooks worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="49cd9-105">Deze nieuwe mogelijkheid kunt u automatisch uit te voeren standaard in reactie op waarschuwingen van de virtuele machine, zoals het opnieuw te starten of stoppen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49cd9-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="49cd9-106">Voorheen tijdens het maken van de waarschuwingsregel VM kon u [opgeven van een Automation-webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) aan een runbook om uit te voeren van het runbook wanneer de waarschuwing is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="49cd9-107">Maar vereist dit dat u voor het werk van het maken van het runbook, maken van de webhook voor het runbook en klik vervolgens kopiëren en plakken van de webhook tijdens het maken van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="49cd9-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="49cd9-108">Met deze nieuwe versie is het proces is veel eenvoudiger omdat u een runbook rechtstreeks uit een lijst tijdens het maken van de waarschuwingsregel kiezen kunt en kunt u een automatiseringsaccount dat wordt uitgevoerd van het runbook of eenvoudig een account maken.</span><span class="sxs-lookup"><span data-stu-id="49cd9-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="49cd9-109">In dit artikel ziet we u hoe eenvoudig het is een Azure VM-waarschuwing instellen en configureren van een Automation-runbook moet worden uitgevoerd als de waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="49cd9-110">Voorbeeldscenario's bevatten een virtuele machine opnieuw te starten wanneer het geheugengebruik sommige als gevolg van een toepassing op de virtuele machine met een geheugenlek overschrijdt of een virtuele machine stoppen wanneer de gebruiker CPU-tijd minder dan 1% voor het afgelopen uur is en niet gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="49cd9-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="49cd9-111">Ook wordt uitgelegd hoe het automatisch maken van een service-principal in uw Automation-account vereenvoudigt het gebruik van runbooks in Azure waarschuwing herbemiddeling.</span><span class="sxs-lookup"><span data-stu-id="49cd9-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="49cd9-112">Een waarschuwing op een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="49cd9-112">Create an alert on a VM</span></span>
<span data-ttu-id="49cd9-113">Voer de volgende stappen uit voor het configureren van een waarschuwing als u wilt een runbook starten wanneer de drempel is voldaan.</span><span class="sxs-lookup"><span data-stu-id="49cd9-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="49cd9-114">Met deze release alleen wordt ondersteund V2 virtuele machines en ondersteuning voor klassieke die virtuele machines wordt binnenkort toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="49cd9-115">Aanmelden bij de Azure-portal en klikt u op **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="49cd9-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="49cd9-116">Selecteer een van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="49cd9-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="49cd9-117">De virtuele machine dashboard blade wordt weergegeven en de **instellingen** blade rechts ervan.</span><span class="sxs-lookup"><span data-stu-id="49cd9-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="49cd9-118">Van de **instellingen** blade onder de sectie bewaking selecteren **waarschuwing regels**.</span><span class="sxs-lookup"><span data-stu-id="49cd9-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="49cd9-119">Op de **waarschuwing regels** blade, klikt u op **waarschuwing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="49cd9-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="49cd9-120">Hiermee opent u de **een waarschuwingsregel toevoegen** blade kunt u de voorwaarden voor de waarschuwing configureren en kiezen uit een of alle van de volgende opties: e-mailbericht verzenden naar iemand, gebruikt u een webhook om de waarschuwing naar een ander systeem doorsturen en/of een Automation-runbook worden uitgevoerd in reactie poging tot het probleem te herstellen.</span><span class="sxs-lookup"><span data-stu-id="49cd9-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="49cd9-121">Een runbook configureren</span><span class="sxs-lookup"><span data-stu-id="49cd9-121">Configure a runbook</span></span>
<span data-ttu-id="49cd9-122">Selecteer voor het configureren van een runbook worden uitgevoerd wanneer de waarschuwingsdrempel van de VM wordt voldaan, **Automation-Runbook**.</span><span class="sxs-lookup"><span data-stu-id="49cd9-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="49cd9-123">In de **runbook configureren** blade kunt u het runbook nu wordt uitgevoerd en het Automation-account voor het uitvoeren van het runbook in.</span><span class="sxs-lookup"><span data-stu-id="49cd9-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![Configureer een Automation-runbook en een nieuw Automation-Account maken](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="49cd9-125">Voor deze release kunt u kiezen uit drie runbooks waarmee de service – VM starten, stoppen VM of VM verwijderen (verwijderen).</span><span class="sxs-lookup"><span data-stu-id="49cd9-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="49cd9-126">De mogelijkheid om te selecteren van andere runbooks of een van uw eigen runbooks zijn beschikbaar in een toekomstige release.</span><span class="sxs-lookup"><span data-stu-id="49cd9-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbooks kiezen](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="49cd9-128">Nadat u een van de drie beschikbare runbooks, selecteert de **Automation-account** vervolgkeuzelijst wordt weergegeven en kunt u een automation-account als het runbook wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="49cd9-129">Runbooks moeten worden uitgevoerd in de context van een [Automation-account](automation-security-overview.md) die zich in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="49cd9-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="49cd9-130">U kunt een Automation-account dat u al hebt gemaakt, of u kunt een nieuw Automation-account voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="49cd9-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="49cd9-131">De runbooks die worden geleverd worden geverifieerd bij Azure met behulp van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="49cd9-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="49cd9-132">Als u kiest voor het uitvoeren van het runbook in een van uw bestaande Automation-accounts, wordt we automatisch de service principal voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="49cd9-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="49cd9-133">Als u een nieuw automatiseringsaccount maakt, maakt wordt automatisch het account en de service-principal.</span><span class="sxs-lookup"><span data-stu-id="49cd9-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="49cd9-134">In beide gevallen twee activa ook worden gemaakt in het Automation-account: de activa van een certificaat met de naam **AzureRunAsCertificate** en de activa van een verbinding met de naam **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="49cd9-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="49cd9-135">De runbooks gebruikt **AzureRunAsConnection** te verifiëren bij Azure om de actie voor beheer op basis van de virtuele machine uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="49cd9-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="49cd9-136">De service-principal in het abonnementsbereik wordt gemaakt en is de rol Inzender toegewezen.</span><span class="sxs-lookup"><span data-stu-id="49cd9-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="49cd9-137">Deze rol is vereist om het account moet gemachtigd zijn om uit te voeren van Automation-runbooks voor het beheren van virtuele Azure-machines.</span><span class="sxs-lookup"><span data-stu-id="49cd9-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="49cd9-138">Het maken van een account Automaton en/of de service-principal is een eenmalige gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="49cd9-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="49cd9-139">Zodra ze zijn gemaakt, kunt u dat account kunt gebruiken voor het uitvoeren van runbooks voor andere virtuele machine van Azure-waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="49cd9-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="49cd9-140">Wanneer u klikt op **OK** de waarschuwing is geconfigureerd en als u de optie voor het maken van een nieuw automatiseringsaccount hebt geselecteerd, samen met de service-principal wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="49cd9-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="49cd9-141">Dit kan enkele seconden duren.</span><span class="sxs-lookup"><span data-stu-id="49cd9-141">This can take a few seconds to complete.</span></span>  

![Runbook wordt geconfigureerd](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="49cd9-143">Nadat de configuratie is voltooid ziet u de naam van het runbook worden weergegeven in de **een waarschuwingsregel toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="49cd9-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Runbook is geconfigureerd](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="49cd9-145">Klik op **OK** in de **een waarschuwingsregel toevoegen** blade en de waarschuwingsregel wordt gemaakt en wordt geactiveerd als de virtuele machine actief is.</span><span class="sxs-lookup"><span data-stu-id="49cd9-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="49cd9-146">In- of uitschakelen van een runbook</span><span class="sxs-lookup"><span data-stu-id="49cd9-146">Enable or disable a runbook</span></span>
<span data-ttu-id="49cd9-147">Als u een runbook dat is geconfigureerd voor een waarschuwing hebt, kunt u deze uitschakelen zonder te verwijderen van de runbookconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="49cd9-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="49cd9-148">Hiermee kunt u de waarschuwing actief houden en testen mogelijk enkele van de regels voor waarschuwingen en later opnieuw inschakelen het runbook.</span><span class="sxs-lookup"><span data-stu-id="49cd9-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="49cd9-149">Een runbook maken dat met een Azure-waarschuwing werkt</span><span class="sxs-lookup"><span data-stu-id="49cd9-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="49cd9-150">Wanneer u een runbook als onderdeel van een Azure waarschuwingsregel kiest, moet het runbook bevatten logica voor het beheren van de gegevens van de waarschuwing die wordt doorgegeven aan deze.</span><span class="sxs-lookup"><span data-stu-id="49cd9-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="49cd9-151">Wanneer een runbook is geconfigureerd in een waarschuwingsregel, is een webhook gemaakt voor het runbook; Deze webhook wordt vervolgens gebruikt voor het runbook starten elke keer dat de waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="49cd9-152">De werkelijke aanroep naar start het runbook is een HTTP POST-aanvraag naar de webhook-URL.</span><span class="sxs-lookup"><span data-stu-id="49cd9-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="49cd9-153">De hoofdtekst van de POST-aanvraag bevat een JSON-indeling object dat nuttige eigenschappen die betrekking hebben op de waarschuwing bevat.</span><span class="sxs-lookup"><span data-stu-id="49cd9-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="49cd9-154">Zoals u hieronder zien kunt, bevat de waarschuwingsgegevens-gegevens, zoals de abonnements-id, resourceGroupName resourceName en resourceType.</span><span class="sxs-lookup"><span data-stu-id="49cd9-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="49cd9-155">Voorbeeld van waarschuwingsgegevens</span><span class="sxs-lookup"><span data-stu-id="49cd9-155">Example of Alert data</span></span>
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

<span data-ttu-id="49cd9-156">Wanneer de service Automation-webhook het HTTP POST-protocol ontvangt haalt gegevens van de waarschuwing en wordt doorgegeven aan het runbook in de WebhookData runbook-invoerparameter.</span><span class="sxs-lookup"><span data-stu-id="49cd9-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="49cd9-157">Hieronder ziet u een voorbeeldrunbook dat laat hoe gebruikt u de parameter WebhookData zien en ophalen van gegevens van de waarschuwing en deze gebruiken voor het beheren van de Azure resource die de waarschuwing heeft geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="49cd9-158">Voorbeeldrunbook</span><span class="sxs-lookup"><span data-stu-id="49cd9-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="49cd9-159">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="49cd9-159">Summary</span></span>
<span data-ttu-id="49cd9-160">Wanneer u een waarschuwing op een virtuele machine in Azure configureert, hebt u nu de mogelijkheid voor het configureren van eenvoudig een Automation-runbook om de herstelactie automatisch worden uitgevoerd wanneer de waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="49cd9-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="49cd9-161">Voor deze release kunt u kiezen uit runbooks te starten, stoppen of verwijderen van een virtuele machine, afhankelijk van uw waarschuwing scenario.</span><span class="sxs-lookup"><span data-stu-id="49cd9-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="49cd9-162">Dit is slechts een begin van het inschakelen van scenario's waarin u de acties die automatisch worden uitgevoerd wanneer een waarschuwing wordt geactiveerd (melding, het oplossen van problemen herstel) beheren.</span><span class="sxs-lookup"><span data-stu-id="49cd9-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49cd9-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49cd9-163">Next Steps</span></span>
* <span data-ttu-id="49cd9-164">Zie [Mijn eerste grafische runbook](automation-first-runbook-graphical.md) om aan de slag te gaan met grafische runbooks</span><span class="sxs-lookup"><span data-stu-id="49cd9-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="49cd9-165">Zie [Mijn eerste PowerShell Workflow-runbook](automation-first-runbook-textual.md) om aan de slag te gaan met PowerShell Workflow-runbooks</span><span class="sxs-lookup"><span data-stu-id="49cd9-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="49cd9-166">Zie [Azure Automation-runbooktypen](automation-runbook-types.md) voor meer informatie over runbooktypen, hun voordelen en beperkingen</span><span class="sxs-lookup"><span data-stu-id="49cd9-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

