---
title: aaaLog Analytics-functies voor serviceproviders | Microsoft Docs
description: Log Analytics kunt beheerd serviceproviders (MSPs) grote ondernemingen Independent Software Vendors (ISV's) en hosting serviceproviders beheren en bewaken van servers in een van de klant on-premises of cloudinfrastructuur.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Log Analytics-functies voor serviceproviders
Log Analytics kunt beheerde serviceproviders (MSPs), grote ondernemingen, onafhankelijke softwareleveranciers (ISV's) en hosting serviceproviders beheren en bewaken van servers in een van de klant on-premises of cloudinfrastructuur. 

Grote ondernemingen delen veel overeenkomsten met serviceproviders, vooral wanneer u een centrale IT-team dat verantwoordelijk is voor het beheren van IT voor veel verschillende bedrijfseenheden. Voor het gemak, wordt dit document Hallo term *serviceprovider* maar hello dezelfde functionaliteit is ook beschikbaar voor ondernemingen en andere klanten.

## <a name="cloud-solution-provider"></a>Cloud Solution Provider
Voor partners en serviceproviders die deel van Hallo uitmaken [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) programma, Log Analytics is een van de hello Azure-services beschikbaar is op een CSP-abonnement. 

Log Analytics Hallo na mogelijkheden zijn ingeschakeld in *Cloud Solution Provider* abonnementen.

Als een *Cloud Solution Provider* kunt u:

* Log Analytics-werkruimten maken in een tenant (de klant) abonnement.
* Access-werkruimten die zijn gemaakt door tenants. 
* Toevoegen en verwijderen van de gebruiker toegang toohello werkruimte met behulp van Azure Gebruikersbeheer. Wanneer in een tenant-werkruimte van Hallo OMS portal Hallo pagina Gebruikersbeheer onder instellingen niet beschikbaar is
  * Log Analytics biedt geen ondersteuning voor op rollen gebaseerde toegang nog -zodat een gebruiker `reader` toestemming in hello Azure-portal kan ze toomake configuratiewijzigingen in Hallo OMS-portal

toolog in tooa tenantabonnement, moet u toospecify hello tenant-id. Hallo tenant-id is vaak het laatste onderdeel van Hallo e-mailadres gebruikt toosign in.

* Voeg in Hallo OMS-portal `?tenant=contoso.com` in Hallo-URL voor Hallo-portal. Bijvoorbeeld: `mms.microsoft.com/?tenant=contoso.com`
* Gebruik in PowerShell Hallo `-Tenant contoso.com` parameter wanneer u `Add-AzureRmAccount` cmdlet
* Hallo tenant-id wordt automatisch toegevoegd wanneer u Hallo `OMS portal` koppelen vanuit Azure portal tooopen hello en meld u toohello OMS-portal voor werkruimte Hallo geselecteerd

Als een *klant* van een Cloud Solution Provider die u kunt:

* Log analytics-werkruimten maken in een CSP-abonnement
* Toegang tot werkruimten die zijn gemaakt door Hallo CSP
  * Gebruik Hallo `OMS portal` koppelen vanuit Azure portal tooopen hello en meld u toohello OMS-portal voor werkruimte Hallo geselecteerd
* Weergeven en gebruiken van Hallo pagina Gebruikersbeheer onder de instellingen in Hallo OMS-portal

> [!NOTE]
> Hallo opgenomen back-up- en Site Recovery-oplossingen voor logboekanalyse niet kunnen tooconnect tooa Recovery Services-kluis en kunnen niet worden geconfigureerd in een CSP-abonnement. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Het beheren van meerdere klanten met Log Analytics
Het wordt aanbevolen dat u een werkruimte voor logboekanalyse maken voor elke klant die u beheert. Een werkruimte voor logboekanalyse biedt:

* Een geografische locatie voor gegevens toobe opgeslagen. 
* Details voor facturering 
* Gegevensisolatie 
* Unieke configuratie

Als u een werkruimte per klant maakt, kunnen tookeep zijn de gegevens van elke klant afzonderlijke en ook bijhouden Hallo gebruik van elke klant.

Meer informatie over wanneer en waarom toocreate meerdere werkruimten wordt beschreven in [toegang toolog analytics beheren](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Maken en de configuratie van de klant werkruimten kunnen worden geautomatiseerd met [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager-sjablonen](log-analytics-template-workspace-configuration.md), of met behulp van Hallo [REST-API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

Hallo-gebruik van Resource Manager-sjablonen voor de configuratie van de werkruimte kunt u toohave een master-configuratie die kan worden gebruikt toocreate en werkruimten configureren. U kunt altijd zeker weet dat als werkruimten worden gemaakt voor klanten dat ze automatisch worden tooyour vereisten geconfigureerd. Tijdens het bijwerken van de vereisten van uw sjabloon Hallo bijgewerkt en worden vervolgens opnieuw toegepast Hallo bestaande werkruimten. Dit proces zorgt ervoor dat uw nieuwe standaarden voldoen aan de zelfs bestaande werkruimten.    

Wanneer het beheer van meerdere Log Analytics-werkruimten, raden we aan elke werkruimte integreren met uw bestaande ticketsysteem gebruikt / operations-console met behulp van Hallo [waarschuwingen](log-analytics-alerts.md) functionaliteit. Door te integreren met uw bestaande systemen, kunnen ondersteuningsmedewerkers blijven toofollow hun bekend processen. Log Analytics regelmatig gecontroleerd elke werkruimte tegen Hallo waarschuwing criteria die u opgeeft en genereert een waarschuwing wanneer de actie te ondernemen.

Gebruik voor aangepaste weergaven van gegevens Hallo [dashboard](../azure-portal/azure-portal-dashboards.md) mogelijkheden in hello Azure-portal.  

Voor executive niveau rapporten waarin gegevens worden samengevat in werkruimten kunt u de integratie tussen logboekanalyse Hallo en [PowerBI](log-analytics-powerbi.md). Als u toointegrate met een andere rapportagesysteem nodig hebt, kunt u Hallo-API van zoekservice (via PowerShell of [REST](log-analytics-log-search-api.md)) toorun query's en exporteren van de zoekresultaten.

## <a name="next-steps"></a>Volgende stappen
* Het maken en de configuratie van werkruimten met automatiseren [Resource Manager-sjablonen](log-analytics-template-workspace-configuration.md)
* Het maken van werkruimten met automatiseren [PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Gebruik [waarschuwingen](log-analytics-alerts.md) toointegrate met bestaande systemen
* Samenvatting rapporten genereren met de [Power BI](log-analytics-powerbi.md)

