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
# <a name="azure-log-integration-faq"></a>Veelgestelde vragen over Azure-logboekanalyse-integratie
Dit artikel worden veelgestelde vragen (FAQ) over de integratie van Azure Log. 

Integratie van Azure Log is een Windows-besturingssysteemservice waarmee u de onbewerkte logboeken toointegrate van uw Azure-resources in uw on-premises security information en event management (SIEM) systemen kunt. Deze integratie biedt een uniforme dashboard voor alle activa, lokaal of in Hallo cloud. U kunt vervolgens samenvoegen, correleren, analyseren en waarschuwen voor beveiligingsgebeurtenissen die zijn gekoppeld aan uw toepassingen.

## <a name="is-hello-azure-log-integration-software-free"></a>Is hello Azure Log integratie software gratis?
Ja. Er zijn geen kosten voor hello Azure Log integratie software.

## <a name="where-is-azure-log-integration-available"></a>Waar Azure Log integratie beschikbaar is?

Het is momenteel beschikbaar zijn in Azure commerciële en Azure Government en is niet beschikbaar in China of Duitsland.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Hoe kan ik Hallo waarin Azure Log-integratie is binnenhalen van Logboeken van de virtuele machine van Azure storage-accounts zien?
Hallo-opdracht uitvoeren **azlog bronlijst**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>Hoe weet ik welke abonnement Hallo integratie van Azure Log logboeken zijn van

In geval van controlelogboeken die worden geplaatst in Hallo Hallo **AzureResourcemanagerJson** -adreslijsten, Hallo abonnements-ID is in de logboekbestandsnaam Hallo. Dit geldt ook voor logboeken in Hallo **AzureSecurityCenterJson** map. Bijvoorbeeld:

20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Azure Active Directory-controlelogboeken bevatten Hallo tenant-ID als deel van naam Hallo.

Diagnostische logboeken die in een event hub worden gelezen opnemen Hallo abonnements-ID als deel van naam Hallo niet. In plaats daarvan bevatten ze Hallo beschrijvende naam die is opgegeven als onderdeel van Hallo maken van de hub gebeurtenisbron Hallo. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Hoe kan ik Hallo proxyconfiguratie bijwerken?
Als de proxy-instellingen kan geen toegang tot Azure-opslag rechtstreeks, open Hallo **AZLOG. EXE. CONFIG** bestanden per **c:\Program Files\Microsoft Azure Log integratie**. Update Hallo bestand tooinclude hello **defaultProxy** sectie met Hallo proxyadres van uw organisatie. Nadat het Hallo-update is voltooid, service stoppen en starten Hallo met behulp van opdrachten Hallo **net stop azlog** en **net start azlog**.

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>Hoe kan ik de abonnementsgegevens Hallo in Windows-gebeurtenissen weergeven?
Hallo abonnement-ID toohello beschrijvende naam toevoegen tijdens het Hallo-bron toevoegen:

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
Hallo gebeurtenis XML heeft Hallo metagegevens, met inbegrip van Hallo abonnements-ID te volgen:

![XML-gebeurtenis][1]

## <a name="error-messages"></a>Foutberichten
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Wanneer ik Hallo-opdracht uitvoert **azlog createazureid**, waarom krijg ik de volgende fout Hallo?
Fout:

  *Kan niet toocreate AAD-toepassing - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - reden = 'Verboden' - bericht = 'onvoldoende bevoegdheden toocomplete Hallo bewerking'.*

Hallo **azlog createazureid** opdracht wordt geprobeerd een service-principal in alle hello Azure AD-tenants voor Hallo-abonnementen die hello Azure-aanmelding toegang tot heeft toocreate. Als uw Azure-aanmelding alleen een gastgebruiker in die Azure AD-tenant is, mislukt de Hallo-opdracht met 'onvoldoende bevoegdheden toocomplete Hallo bewerking'. Hallo tenant admin tooadd vraag uw account als een gebruiker in Hallo-tenant.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Wanneer ik Hallo-opdracht uitvoert **azlog autoriseren**, waarom krijg ik de volgende fout Hallo?
Fout:

  *Waarschuwing voor het maken van roltoewijzing - AuthorizationFailed: Hallo client janedo@microsoft.com' met object-id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' geen autorisatie tooperform actie 'Microsoft.Authorization/roleAssignments/write' bereik ' / abonnementen, 70-d 95299-d689-4c 97 b971 0d8ff0000000'.*

Hallo **azlog autoriseren** opdracht wordt toegewezen rol van lezer toohello Azure AD-service-principal Hallo (gemaakt met **azlog createazureid**) toohello opgegeven abonnementen. Als hello Azure-aanmelding niet een CO-beheerder of een eigenaar van het Hallo-abonnement, mislukt dit met een foutbericht 'Autorisatie is mislukt'. Azure op rollen gebaseerde toegangsbeheer (RBAC) van CO-beheerder of de eigenaar is de benodigde toocomplete deze actie.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Waar vind ik Hallo definitie van Hallo eigenschappen in het controlelogboek Hallo
Zie:

* [Bewerkingen met Azure Resource Manager controleren](../azure-resource-manager/resource-group-audit.md)
* [Lijst Hallo management gebeurtenissen in een abonnement in hello Azure Monitor REST-API](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Waar vind ik meer informatie over Azure Security Center alerts
Zie [beheren en reageert toosecurity waarschuwingen in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>Hoe kan ik wijzigen wat met VM diagnostische gegevens worden verzameld?
Zie voor meer informatie over hoe tooget, wijzigen en stel de configuratie van Azure Diagnostics hello, [Gebruik PowerShell tooenable diagnostische Azure-gegevens in een virtuele machine met Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hallo volgt opgehaald hello Azure Diagnostics configuratie:

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

Hallo volgt wijzigen hello Azure Diagnostics-configuratie. In deze configuratie worden alleen gebeurtenis-ID 4624 en gebeurtenis-ID 4625 verzameld van het beveiligingslogboek Hallo. Microsoft Antimalware voor Azure gebeurtenissen worden verzameld van het logboek met systeemgebeurtenissen Hallo. Zie voor meer informatie over Hallo gebruik van XPath-expressies [verbruikt gebeurtenissen](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Hallo wordt volgende voorbeeld hello Azure Diagnostics configuratie:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

Nadat u wijzigingen aanbrengt, controleert u Hallo storage account tooensure die Hallo juist gebeurtenissen worden verzameld.

Als u problemen tijdens het Hallo-installatie en configuratie hebt, opent u een [ondersteuningsaanvraag](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Selecteer **logboek integratie** als Hallo service waarvoor u ondersteuning aanvraagt.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>Kan ik Azure Log integratie toointegrate netwerk-Watcher Logboeken in mijn SIEM gebruiken?

Azure-netwerk-Watcher wordt grote hoeveelheden van de logboekgegevens gegenereerd. Deze logboeken zijn niet geschikt toobe verzonden tooa SIEM. doel van de Hallo alleen ondersteund voor netwerk-Watcher Logboeken is een opslagaccount. Integratie van Azure Log biedt geen ondersteuning voor het lezen van deze logboeken en ze beschikbaar tooa SIEM.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
