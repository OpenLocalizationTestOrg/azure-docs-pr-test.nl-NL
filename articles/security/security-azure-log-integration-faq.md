---
title: Veelgestelde vragen over het logboek integratie aaaAzure | Microsoft Docs
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
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="2b38c-103">Veelgestelde vragen over Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="2b38c-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="2b38c-104">Dit artikel worden veelgestelde vragen (FAQ) over de integratie van Azure Log.</span><span class="sxs-lookup"><span data-stu-id="2b38c-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="2b38c-105">Integratie van Azure Log is een Windows-besturingssysteemservice waarmee u de onbewerkte logboeken toointegrate van uw Azure-resources in uw on-premises security information en event management (SIEM) systemen kunt.</span><span class="sxs-lookup"><span data-stu-id="2b38c-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="2b38c-106">Deze integratie biedt een uniforme dashboard voor alle activa, lokaal of in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="2b38c-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="2b38c-107">U kunt vervolgens samenvoegen, correleren, analyseren en waarschuwen voor beveiligingsgebeurtenissen die zijn gekoppeld aan uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2b38c-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="2b38c-108">Is hello Azure Log integratie software gratis?</span><span class="sxs-lookup"><span data-stu-id="2b38c-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="2b38c-109">Ja.</span><span class="sxs-lookup"><span data-stu-id="2b38c-109">Yes.</span></span> <span data-ttu-id="2b38c-110">Er zijn geen kosten voor hello Azure Log integratie software.</span><span class="sxs-lookup"><span data-stu-id="2b38c-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="2b38c-111">Waar Azure Log integratie beschikbaar is?</span><span class="sxs-lookup"><span data-stu-id="2b38c-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="2b38c-112">Het is momenteel beschikbaar zijn in Azure commerciële en Azure Government en is niet beschikbaar in China of Duitsland.</span><span class="sxs-lookup"><span data-stu-id="2b38c-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="2b38c-113">Hoe kan ik Hallo waarin Azure Log-integratie is binnenhalen van Logboeken van de virtuele machine van Azure storage-accounts zien?</span><span class="sxs-lookup"><span data-stu-id="2b38c-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="2b38c-114">Hallo-opdracht uitvoeren **azlog bronlijst**.</span><span class="sxs-lookup"><span data-stu-id="2b38c-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="2b38c-115">Hoe weet ik welke abonnement Hallo integratie van Azure Log logboeken zijn van</span><span class="sxs-lookup"><span data-stu-id="2b38c-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="2b38c-116">In geval van controlelogboeken die worden geplaatst in Hallo Hallo **AzureResourcemanagerJson** -adreslijsten, Hallo abonnements-ID is in de logboekbestandsnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b38c-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="2b38c-117">Dit geldt ook voor logboeken in Hallo **AzureSecurityCenterJson** map.</span><span class="sxs-lookup"><span data-stu-id="2b38c-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="2b38c-118">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2b38c-118">For example:</span></span>

<span data-ttu-id="2b38c-119">20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="2b38c-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="2b38c-120">Azure Active Directory-controlelogboeken bevatten Hallo tenant-ID als deel van naam Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b38c-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="2b38c-121">Diagnostische logboeken die in een event hub worden gelezen opnemen Hallo abonnements-ID als deel van naam Hallo niet.</span><span class="sxs-lookup"><span data-stu-id="2b38c-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="2b38c-122">In plaats daarvan bevatten ze Hallo beschrijvende naam die is opgegeven als onderdeel van Hallo maken van de hub gebeurtenisbron Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b38c-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="2b38c-123">Hoe kan ik Hallo proxyconfiguratie bijwerken?</span><span class="sxs-lookup"><span data-stu-id="2b38c-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="2b38c-124">Als de proxy-instellingen kan geen toegang tot Azure-opslag rechtstreeks, open Hallo **AZLOG. EXE. CONFIG** bestanden per **c:\Program Files\Microsoft Azure Log integratie**.</span><span class="sxs-lookup"><span data-stu-id="2b38c-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="2b38c-125">Update Hallo bestand tooinclude hello **defaultProxy** sectie met Hallo proxyadres van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="2b38c-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="2b38c-126">Nadat het Hallo-update is voltooid, service stoppen en starten Hallo met behulp van opdrachten Hallo **net stop azlog** en **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="2b38c-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="2b38c-127">Hoe kan ik de abonnementsgegevens Hallo in Windows-gebeurtenissen weergeven?</span><span class="sxs-lookup"><span data-stu-id="2b38c-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="2b38c-128">Hallo abonnement-ID toohello beschrijvende naam toevoegen tijdens het Hallo-bron toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2b38c-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="2b38c-129">Hallo gebeurtenis XML heeft Hallo metagegevens, met inbegrip van Hallo abonnements-ID te volgen:</span><span class="sxs-lookup"><span data-stu-id="2b38c-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![XML-gebeurtenis][1]

## <a name="error-messages"></a><span data-ttu-id="2b38c-131">Foutberichten</span><span class="sxs-lookup"><span data-stu-id="2b38c-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="2b38c-132">Wanneer ik Hallo-opdracht uitvoert **azlog createazureid**, waarom krijg ik de volgende fout Hallo?</span><span class="sxs-lookup"><span data-stu-id="2b38c-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="2b38c-133">Fout:</span><span class="sxs-lookup"><span data-stu-id="2b38c-133">Error:</span></span>

  <span data-ttu-id="2b38c-134">*Kan niet toocreate AAD-toepassing - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - reden = 'Verboden' - bericht = 'onvoldoende bevoegdheden toocomplete Hallo bewerking'.*</span><span class="sxs-lookup"><span data-stu-id="2b38c-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="2b38c-135">Hallo **azlog createazureid** opdracht wordt geprobeerd een service-principal in alle hello Azure AD-tenants voor Hallo-abonnementen die hello Azure-aanmelding toegang tot heeft toocreate.</span><span class="sxs-lookup"><span data-stu-id="2b38c-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="2b38c-136">Als uw Azure-aanmelding alleen een gastgebruiker in die Azure AD-tenant is, mislukt de Hallo-opdracht met 'onvoldoende bevoegdheden toocomplete Hallo bewerking'.</span><span class="sxs-lookup"><span data-stu-id="2b38c-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="2b38c-137">Hallo tenant admin tooadd vraag uw account als een gebruiker in Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="2b38c-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="2b38c-138">Wanneer ik Hallo-opdracht uitvoert **azlog autoriseren**, waarom krijg ik de volgende fout Hallo?</span><span class="sxs-lookup"><span data-stu-id="2b38c-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="2b38c-139">Fout:</span><span class="sxs-lookup"><span data-stu-id="2b38c-139">Error:</span></span>

  <span data-ttu-id="2b38c-140">*Waarschuwing voor het maken van roltoewijzing - AuthorizationFailed: Hallo client janedo@microsoft.com' met object-id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' geen autorisatie tooperform actie 'Microsoft.Authorization/roleAssignments/write' bereik ' / abonnementen, 70-d 95299-d689-4c 97 b971 0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="2b38c-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="2b38c-141">Hallo **azlog autoriseren** opdracht wordt toegewezen rol van lezer toohello Azure AD-service-principal Hallo (gemaakt met **azlog createazureid**) toohello opgegeven abonnementen.</span><span class="sxs-lookup"><span data-stu-id="2b38c-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="2b38c-142">Als hello Azure-aanmelding niet een CO-beheerder of een eigenaar van het Hallo-abonnement, mislukt dit met een foutbericht 'Autorisatie is mislukt'.</span><span class="sxs-lookup"><span data-stu-id="2b38c-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="2b38c-143">Azure op rollen gebaseerde toegangsbeheer (RBAC) van CO-beheerder of de eigenaar is de benodigde toocomplete deze actie.</span><span class="sxs-lookup"><span data-stu-id="2b38c-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="2b38c-144">Waar vind ik Hallo definitie van Hallo eigenschappen in het controlelogboek Hallo</span><span class="sxs-lookup"><span data-stu-id="2b38c-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="2b38c-145">Zie:</span><span class="sxs-lookup"><span data-stu-id="2b38c-145">See:</span></span>

* [<span data-ttu-id="2b38c-146">Bewerkingen met Azure Resource Manager controleren</span><span class="sxs-lookup"><span data-stu-id="2b38c-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="2b38c-147">Lijst Hallo management gebeurtenissen in een abonnement in hello Azure Monitor REST-API</span><span class="sxs-lookup"><span data-stu-id="2b38c-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="2b38c-148">Waar vind ik meer informatie over Azure Security Center alerts</span><span class="sxs-lookup"><span data-stu-id="2b38c-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="2b38c-149">Zie [beheren en reageert toosecurity waarschuwingen in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2b38c-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="2b38c-150">Hoe kan ik wijzigen wat met VM diagnostische gegevens worden verzameld?</span><span class="sxs-lookup"><span data-stu-id="2b38c-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="2b38c-151">Zie voor meer informatie over hoe tooget, wijzigen en stel de configuratie van Azure Diagnostics hello, [Gebruik PowerShell tooenable diagnostische Azure-gegevens in een virtuele machine met Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b38c-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="2b38c-152">Hallo volgt opgehaald hello Azure Diagnostics configuratie:</span><span class="sxs-lookup"><span data-stu-id="2b38c-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="2b38c-153">Hallo volgt wijzigen hello Azure Diagnostics-configuratie.</span><span class="sxs-lookup"><span data-stu-id="2b38c-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="2b38c-154">In deze configuratie worden alleen gebeurtenis-ID 4624 en gebeurtenis-ID 4625 verzameld van het beveiligingslogboek Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b38c-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="2b38c-155">Microsoft Antimalware voor Azure gebeurtenissen worden verzameld van het logboek met systeemgebeurtenissen Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b38c-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="2b38c-156">Zie voor meer informatie over Hallo gebruik van XPath-expressies [verbruikt gebeurtenissen](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="2b38c-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="2b38c-157">Hallo wordt volgende voorbeeld hello Azure Diagnostics configuratie:</span><span class="sxs-lookup"><span data-stu-id="2b38c-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="2b38c-158">Nadat u wijzigingen aanbrengt, controleert u Hallo storage account tooensure die Hallo juist gebeurtenissen worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="2b38c-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="2b38c-159">Als u problemen tijdens het Hallo-installatie en configuratie hebt, opent u een [ondersteuningsaanvraag](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="2b38c-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="2b38c-160">Selecteer **logboek integratie** als Hallo service waarvoor u ondersteuning aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="2b38c-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="2b38c-161">Kan ik Azure Log integratie toointegrate netwerk-Watcher Logboeken in mijn SIEM gebruiken?</span><span class="sxs-lookup"><span data-stu-id="2b38c-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="2b38c-162">Azure-netwerk-Watcher wordt grote hoeveelheden van de logboekgegevens gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2b38c-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="2b38c-163">Deze logboeken zijn niet geschikt toobe verzonden tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="2b38c-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="2b38c-164">doel van de Hallo alleen ondersteund voor netwerk-Watcher Logboeken is een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2b38c-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="2b38c-165">Integratie van Azure Log biedt geen ondersteuning voor het lezen van deze logboeken en ze beschikbaar tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="2b38c-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
