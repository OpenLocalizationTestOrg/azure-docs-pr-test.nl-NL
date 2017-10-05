---
title: Veelgestelde vragen over Azure-logboekanalyse-integratie | Microsoft Docs
description: In dit artikel antwoorden op vragen over Azure Log-integratie.
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: bfdc7154160bb6bb7dc9c46eb2352ce74310c4de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="6988b-103">Veelgestelde vragen over Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="6988b-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="6988b-104">Dit artikel worden veelgestelde vragen (FAQ) over de integratie van Azure Log.</span><span class="sxs-lookup"><span data-stu-id="6988b-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="6988b-105">Integratie van Azure Log is een service voor het besturingssysteem van Windows die u gebruiken kunt voor het integreren van onbewerkte logboeken van uw Azure-resources in uw on-premises security information en event management (SIEM) systemen.</span><span class="sxs-lookup"><span data-stu-id="6988b-105">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="6988b-106">Deze integratie biedt een uniforme dashboard voor alle activa, lokaal of in de cloud.</span><span class="sxs-lookup"><span data-stu-id="6988b-106">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span></span> <span data-ttu-id="6988b-107">U kunt vervolgens samenvoegen, correleren, analyseren en waarschuwen voor beveiligingsgebeurtenissen die zijn gekoppeld aan uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6988b-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="6988b-108">Is de software-integratie van Azure Log gratis?</span><span class="sxs-lookup"><span data-stu-id="6988b-108">Is the Azure Log Integration software free?</span></span>
<span data-ttu-id="6988b-109">Ja.</span><span class="sxs-lookup"><span data-stu-id="6988b-109">Yes.</span></span> <span data-ttu-id="6988b-110">Er zijn geen kosten voor de integratie van Azure Log-software.</span><span class="sxs-lookup"><span data-stu-id="6988b-110">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="6988b-111">Waar Azure Log integratie beschikbaar is?</span><span class="sxs-lookup"><span data-stu-id="6988b-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="6988b-112">Het is momenteel beschikbaar zijn in Azure commerciële en Azure Government en is niet beschikbaar in China of Duitsland.</span><span class="sxs-lookup"><span data-stu-id="6988b-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="6988b-113">Hoe kan ik de waarin Azure Log-integratie is binnenhalen van Logboeken van de virtuele machine van Azure storage-accounts zien?</span><span class="sxs-lookup"><span data-stu-id="6988b-113">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="6988b-114">Voer de opdracht **azlog bronlijst**.</span><span class="sxs-lookup"><span data-stu-id="6988b-114">Run the command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-the-azure-log-integration-logs-are-from"></a><span data-ttu-id="6988b-115">Hoe weet ik welke abonnement afkomstig van de logboeken van de integratie van Azure-logboek zijn</span><span class="sxs-lookup"><span data-stu-id="6988b-115">How can I tell which subscription the Azure Log Integration logs are from?</span></span>

<span data-ttu-id="6988b-116">In het geval van controlelogboeken die worden geplaatst in de **AzureResourcemanagerJson** mappen, het abonnement-ID de naam van het logboek wordt.</span><span class="sxs-lookup"><span data-stu-id="6988b-116">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span></span> <span data-ttu-id="6988b-117">Dit geldt ook voor logboeken in de **AzureSecurityCenterJson** map.</span><span class="sxs-lookup"><span data-stu-id="6988b-117">This is also true for logs in the **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="6988b-118">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6988b-118">For example:</span></span>

<span data-ttu-id="6988b-119">20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="6988b-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="6988b-120">Auditlogboeken van Azure Active Directory opnemen als onderdeel van de naam van de tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="6988b-120">Azure Active Directory audit logs include the tenant ID as part of the name.</span></span>

<span data-ttu-id="6988b-121">De abonnements-ID als onderdeel van de naam van de opnemen logboeken met diagnostische gegevens die worden vanuit een event hub gelezen niet.</span><span class="sxs-lookup"><span data-stu-id="6988b-121">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span></span> <span data-ttu-id="6988b-122">Ze bevatten in plaats daarvan de beschrijvende naam die is opgegeven als onderdeel van het maken van de event hub-bron.</span><span class="sxs-lookup"><span data-stu-id="6988b-122">Instead, they include the friendly name specified as part of the creation of the event hub source.</span></span> 

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="6988b-123">Hoe kan ik de proxyconfiguratie bijwerken?</span><span class="sxs-lookup"><span data-stu-id="6988b-123">How can I update the proxy configuration?</span></span>
<span data-ttu-id="6988b-124">Als de proxy-instellingen kan geen toegang tot Azure-opslag rechtstreeks, opent u de **AZLOG. EXE. CONFIG** bestanden per **c:\Program Files\Microsoft Azure Log integratie**.</span><span class="sxs-lookup"><span data-stu-id="6988b-124">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="6988b-125">Bijwerken van het bestand om op te nemen de **defaultProxy** sectie met de proxy-adres van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="6988b-125">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="6988b-126">Nadat de update is voltooid, stoppen en starten van de service met de opdrachten **net stop azlog** en **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="6988b-126">After the update is done, stop and start the service by using the commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="6988b-127">Hoe kan ik informatie over het abonnement in de Windows-gebeurtenissen weergeven?</span><span class="sxs-lookup"><span data-stu-id="6988b-127">How can I see the subscription information in Windows events?</span></span>
<span data-ttu-id="6988b-128">De abonnements-ID toevoegen aan de beschrijvende naam tijdens het toevoegen van de bron:</span><span class="sxs-lookup"><span data-stu-id="6988b-128">Append the subscription ID to the friendly name while adding the source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="6988b-129">De gebeurtenis XML heeft de volgende metagegevens, met inbegrip van de abonnements-ID:</span><span class="sxs-lookup"><span data-stu-id="6988b-129">The event XML has the following metadata, including the subscription ID:</span></span>

![XML-gebeurtenis][1]

## <a name="error-messages"></a><span data-ttu-id="6988b-131">Foutberichten</span><span class="sxs-lookup"><span data-stu-id="6988b-131">Error messages</span></span>
### <a name="when-i-run-the-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="6988b-132">Wanneer ik de opdracht uitvoert **azlog createazureid**, waarom wordt het volgende foutbericht?</span><span class="sxs-lookup"><span data-stu-id="6988b-132">When I run the command **azlog createazureid**, why do I get the following error?</span></span>
<span data-ttu-id="6988b-133">Fout:</span><span class="sxs-lookup"><span data-stu-id="6988b-133">Error:</span></span>

  <span data-ttu-id="6988b-134">*72f988bf-86f1-41af-91ab-2d7cd011db37-reden is mislukt voor het maken van de toepassing van de AAD - Tenant = 'Verboden' - bericht = 'Onvoldoende bevoegdheden om de bewerking te voltooien.'*</span><span class="sxs-lookup"><span data-stu-id="6988b-134">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="6988b-135">De **azlog createazureid** opdracht probeert te maken van een service-principal in de Azure AD-tenants voor de abonnementen die toegang tot de Azure-aanmelding heeft.</span><span class="sxs-lookup"><span data-stu-id="6988b-135">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span></span> <span data-ttu-id="6988b-136">Als uw Azure-aanmelding alleen een gastgebruiker in die Azure AD-tenant is, mislukt de opdracht met "Onvoldoende bevoegdheden om de bewerking te voltooien."</span><span class="sxs-lookup"><span data-stu-id="6988b-136">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span></span> <span data-ttu-id="6988b-137">Vraag de tenantbeheerder aan uw account toevoegen als een gebruiker in de tenant.</span><span class="sxs-lookup"><span data-stu-id="6988b-137">Ask the tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-i-run-the-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="6988b-138">Wanneer ik de opdracht uitvoert **azlog autoriseren**, waarom wordt het volgende foutbericht?</span><span class="sxs-lookup"><span data-stu-id="6988b-138">When I run the command **azlog authorize**, why do I get the following error?</span></span>
<span data-ttu-id="6988b-139">Fout:</span><span class="sxs-lookup"><span data-stu-id="6988b-139">Error:</span></span>

  <span data-ttu-id="6988b-140">*Maken van de roltoewijzing - AuthorizationFailed waarschuwing: de client janedo@microsoft.com' met object-id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' geen autorisatie voor het uitvoeren van de actie 'Microsoft.Authorization/roleAssignments/write' bereik ' / abonnementen, 70-d 95299-d689-4c 97 b971 0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="6988b-140">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="6988b-141">De **azlog autoriseren** opdracht wijst de rol van lezer toe aan de Azure AD-service-principal (gemaakt met **azlog createazureid**) aan de opgegeven abonnementen.</span><span class="sxs-lookup"><span data-stu-id="6988b-141">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span></span> <span data-ttu-id="6988b-142">Als de Azure-aanmelding niet een CO-beheerder of een eigenaar van het abonnement is, mislukt dit met een foutbericht 'Autorisatie is mislukt'.</span><span class="sxs-lookup"><span data-stu-id="6988b-142">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="6988b-143">Azure op rollen gebaseerde toegangsbeheer (RBAC) van CO-beheerder of de eigenaar is nodig om deze actie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="6988b-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-the-audit-log"></a><span data-ttu-id="6988b-144">Waar vind ik de definitie van de eigenschappen in het controlelogboek</span><span class="sxs-lookup"><span data-stu-id="6988b-144">Where can I find the definition of the properties in the audit log?</span></span>
<span data-ttu-id="6988b-145">Zie:</span><span class="sxs-lookup"><span data-stu-id="6988b-145">See:</span></span>

* [<span data-ttu-id="6988b-146">Bewerkingen met Azure Resource Manager controleren</span><span class="sxs-lookup"><span data-stu-id="6988b-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="6988b-147">Lijst van de management-gebeurtenissen in een abonnement in de REST-API van de Azure-Monitor</span><span class="sxs-lookup"><span data-stu-id="6988b-147">List the management events in a subscription in the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="6988b-148">Waar vind ik meer informatie over Azure Security Center alerts</span><span class="sxs-lookup"><span data-stu-id="6988b-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="6988b-149">Zie [beheren en erop reageren beveiligingswaarschuwingen in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6988b-149">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="6988b-150">Hoe kan ik wijzigen wat met VM diagnostische gegevens worden verzameld?</span><span class="sxs-lookup"><span data-stu-id="6988b-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="6988b-151">Zie voor meer informatie over het ophalen, wijzigen en stel de configuratie van de Azure Diagnostics [Gebruik PowerShell voor het inschakelen van Azure Diagnostics in een virtuele machine met Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6988b-151">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="6988b-152">Het volgende voorbeeld wordt de configuratie van Azure Diagnostics:</span><span class="sxs-lookup"><span data-stu-id="6988b-152">The following example gets the Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="6988b-153">Het volgende voorbeeld wijzigt u de configuratie van Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="6988b-153">The following example modifies the Azure Diagnostics configuration.</span></span> <span data-ttu-id="6988b-154">In deze configuratie worden alleen gebeurtenis-ID 4624 en gebeurtenis-ID 4625 verzameld van het beveiligingslogboek.</span><span class="sxs-lookup"><span data-stu-id="6988b-154">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span></span> <span data-ttu-id="6988b-155">Microsoft Antimalware voor Azure gebeurtenissen worden verzameld van het logboek voor systeemgebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="6988b-155">Microsoft Antimalware for Azure events are collected from the system event log.</span></span> <span data-ttu-id="6988b-156">Zie voor meer informatie over het gebruik van XPath-expressies [verbruikt gebeurtenissen](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="6988b-156">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="6988b-157">Het volgende voorbeeld wordt de configuratie van Azure Diagnostics:</span><span class="sxs-lookup"><span data-stu-id="6988b-157">The following example sets the Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="6988b-158">Nadat u wijzigingen aanbrengt, controleert u het opslagaccount om ervoor te zorgen dat de juiste gebeurtenissen worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="6988b-158">After you make changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="6988b-159">Als u problemen tijdens de installatie en configuratie hebt, opent u een [ondersteuningsaanvraag](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="6988b-159">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="6988b-160">Selecteer **logboek integratie** als de service waarvoor u ondersteuning aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="6988b-160">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-to-integrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="6988b-161">Kan ik Azure Log integratie netwerk-Watcher logboeken integreren in mijn SIEM gebruiken?</span><span class="sxs-lookup"><span data-stu-id="6988b-161">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="6988b-162">Azure-netwerk-Watcher wordt grote hoeveelheden van de logboekgegevens gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="6988b-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="6988b-163">Deze logboeken zijn niet bedoeld om te worden verzonden naar een SIEM.</span><span class="sxs-lookup"><span data-stu-id="6988b-163">These logs are not meant to be sent to a SIEM.</span></span> <span data-ttu-id="6988b-164">De enige ondersteunde bestemming voor netwerk-Watcher Logboeken is een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6988b-164">The only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="6988b-165">Integratie van Azure Log biedt geen ondersteuning voor het lezen van deze logboeken en zodat ze beschikbaar zijn in een SIEM.</span><span class="sxs-lookup"><span data-stu-id="6988b-165">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
