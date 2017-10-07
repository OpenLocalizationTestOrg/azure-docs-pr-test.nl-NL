---
title: Resource Manager-Provider bewerkingen aaaAzure | Microsoft Docs
description: Details Hallo bewerkingen die beschikbaar zijn op Hallo Microsoft Azure Resource Manager-resourceproviders
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Azure Resource Manager Resource Provider-bewerkingen

Dit document vindt u Hallo-bewerkingen die beschikbaar zijn voor elke resourceprovider van Microsoft Azure Resource Manager. Deze kunnen worden gebruikt in aangepaste rollen tooprovide gedetailleerde op rollen gebaseerde toegangsbeheer (RBAC) machtigingen tooresources in Azure. Houd er rekening mee dat niet een uitgebreide lijst en bewerkingen kunnen worden toegevoegd of verwijderd als elke provider wordt bijgewerkt. Bewerking tekenreeksen volgt Hallo-indeling van `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Gebruik voor een lijst met uitgebreide en huidige `Get-AzureRmProviderOperation` (in PowerShell) of `azure provider operations show` (in de Azure CLI) toolist bewerkingen van de Azure-resourceproviders.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Bewerking | Beschrijving |
|---|---|
|/ configuration/actie|Configuratie van de Tenant updates.|
|/ services/actie|Een service-exemplaar in Hallo-tenant wordt bijgewerkt.|
|/ configuration/schrijven|De Tenantconfiguratie van een maakt.|
|/Configuration/Read|Hallo Tenantconfiguratie leest.|
|/ services/schrijven|Maakt een service-exemplaar in Hallo-tenant.|
|/Services/Read|Hallo service-exemplaren in Hallo tenant leest.|
|/Services/DELETE|Hiermee verwijdert u een service-exemplaar in Hallo-tenant.|
|/Services/servicemembers/Action|Maakt een exemplaar van de service lid in Hallo-service.|
|/Services/servicemembers/Read|Hallo service lid-exemplaar in Hallo-service worden gelezen.|
|/Services/servicemembers/DELETE|Hiermee verwijdert u een exemplaar van de service lid in Hallo-service.|
|/Services/servicemembers/Alerts/Read|Leest Hallo waarschuwingen voor een lid van de service.|
|/Services/Alerts/Read|Hallo-waarschuwingen voor een service leest.|
|/Services/Alerts/Read|Hallo-waarschuwingen voor een service leest.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Bewerking | Beschrijving |
|---|---|
|/ generateRecommendations/actie|Geeft aanbevelingen|
|/ suppressions/actie|Bijgewerkte suppressions|
|registratie-/ actie|Hallo-abonnement voor Microsoft Advisor Hallo registreert|
|/generateRecommendations/Read|Haalt status aanbevelingen genereren|
|/Recommendations/Read|Leest aanbevelingen|
|/suppressions/Read|Suppressions opgehaald|
|/suppressions/DELETE|Hiermee verwijdert u de onderdrukking|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Bewerking | Beschrijving |
|---|---|
|/servers/Read|Hallo-informatie opgehaald van Hallo opgegeven Analysis Server.|
|servers/schrijven|Gemaakt of bijgewerkt Hallo Analysis-Server opgegeven.|
|/servers/DELETE|Hiermee verwijdert u Hallo Analysis-Server.|
|/servers/Suspend/Action|Onderbreekt Hallo Analysis-Server.|
|/servers/Resume/Action|Hervat hello Analysis-Server.|
|servers/checkNameAvailability<br>/ Action|Controleert dat de opgegeven Analysis Server naam geldig is en niet in gebruik.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Bewerking | Beschrijving |
|---|---|
|/ checkNameAvailability/actie|Controleert of de opgegeven servicenaam is beschikbaar|
|registratie-/ actie|Abonnement voor Microsoft.ApiManagement resourceprovider registreren|
|/ unregister/actie|Abonnement voor Microsoft.ApiManagement resourceprovider van de registratie ongedaan maken|
|/ service/schrijven|Maak een nieuw exemplaar van API Management-Service|
|/Service/Read|Lezen van metagegevens voor een exemplaar van API Management-Service|
|/Service/DELETE|Verwijderen van exemplaar van API Management-Service|
|/Service/updatehostname/Action|Setup, bijwerken of verwijderen van aangepaste domeinnamen voor een API Management-Service|
|/Service/uploadcertificate/Action|SSL-certificaat uploaden voor een API Management-Service|
|/Service/Backup/Action|Back-API Management-Service toohello opgegeven container in een gebruiker opgegeven storage-account|
|/Service/Restore/Action|API Management-Service uit de opgegeven container Hallo in de storage-account opgegeven van een gebruiker herstellen|
|/Service/managedeployments/Action|SKU/eenheden toevoegen of verwijderen van regionale implementaties van API Management-Service wijzigen|
|/Service/getssotoken/Action|SSO-token dat gebruikte toologin in API Management-Service Legacy-portal als een beheerder kan worden opgehaald|
|/Service/applynetworkconfigurationupdates/Action|Updates Hallo Microsoft.ApiManagement resources uitgevoerd in een virtueel netwerk toopick bijgewerkt netwerkinstellingen.|
|/Service/operationresults/Read|Huidige status van een langdurige bewerking opgehaald|
|/Service/networkStatus/Read|Hiermee haalt u Hallo netwerk toegangsstatus van resources.|
|/Service/loggers/Read|Ophalen van lijst met voorkomen of details van berichtenlogboek ophalen|
|/Service/loggers/Write|Nieuwe berichtenlogboek toevoegen of bestaande berichtenlogboek details bijwerken|
|/Service/loggers/DELETE|Bestaande Berichtenlogboek verwijderen|
|/Service/Users/Read|Een lijst met geregistreerde gebruikers of accountdetails van de van een gebruiker ophalen|
|/Service/Users/Write|Een nieuwe gebruiker of de details van de Update-account van een bestaande gebruiker registreren|
|/Service/Users/DELETE|Gebruikersaccount verwijderen|
|/Service/Users/generateSsoUrl/Action|URL SSO genereren. Hallo-URL kan worden gebruikt tooaccess-beheerportal|
|/Service/Users/Subscriptions/Read|Lijst met gebruikersabonnementen ophalen|
|/Service/Users/Keys/Read|Lijst met gebruikerssleutels|
|/Service/Users/Groups/Read|Ophalen van lijst met gebruikersgroepen|
|/Service/tenant/operationResults/Read|Ophalen van lijst met Bewerkingsresultaten of resultaat van een specifieke bewerking ophalen|
|/Service/tenant/Policy/Read|Beleidsconfiguratie van voor Hallo-tenant ophalen|
|/Service/tenant/Policy/Write|Stel de beleidsconfiguratie van voor Hallo tenant|
|/Service/tenant/Policy/DELETE|Configuratie van beleid voor Hallo tenant verwijderen|
|/Service/tenant/Configuration/Save/Action|Hiermee maakt u doorvoeren met configuratie momentopname toohello opgegeven vertakking in Hallo-opslagplaats|
|/Service/tenant/Configuration/Deploy/Action|Hiermee wordt een taak implementatie tooapply wijzigingen Hallo opgegeven git vertakking toohello configuratie in de database.|
|/Service/tenant/Configuration/Validate/Action|Wijzigingen van Hallo opgegeven git vertakking valideert|
|/Service/tenant/Configuration/operationResults/Read|Ophalen van lijst met Bewerkingsresultaten of resultaat van een specifieke bewerking ophalen|
|/Service/tenant/Configuration/syncState/Read|Status van laatste git-synchronisatie ophalen|
|/Service/tenant/Access/Read|Tenant toegang informatie details ophalen|
|/Service/tenant/Access/Write|Tenant toegang informatie details bijwerken|
|/Service/tenant/Access/regeneratePrimaryKey/Action|Primaire sleutel opnieuw genereren|
|/Service/tenant/Access/regenerateSecondaryKey/Action|Secundaire toegangssleutel opnieuw genereren|
|/Service/identityProviders/Read|Ophalen van lijst met identiteitsproviders of Get-details van de identiteitsprovider|
|/Service/identityProviders/Write|Een nieuwe id-Provider of Update details van een bestaande id-Provider maken|
|/Service/identityProviders/DELETE|Bestaande id-Provider verwijderen|
|/Service/Subscriptions/Read|Een lijst met abonnementen product of details van het product abonnement ophalen|
|/Service/Subscriptions/Write|Een bestaande gebruiker tooan bestaand product abonneren of bijwerken van bestaande abonnementsgegevens. Deze bewerking kan worden gebruikt toorenew abonnement|
|/Service/Subscriptions/DELETE|Het abonnement verwijderd. Deze bewerking kan worden gebruikt toodelete abonnement|
|/Service/Subscriptions/regeneratePrimaryKey/Action|Abonnement primaire sleutel opnieuw genereren|
|/Service/Subscriptions/regenerateSecondaryKey/Action|Abonnement secundaire sleutel opnieuw genereren|
|/Service/backends/Read|Ophalen van lijst met back-ends of details van back-end ophalen|
|/Service/backends/Write|Een nieuwe back-end toevoegen of bijwerken van bestaande back-end-details|
|/Service/backends/DELETE|Verwijder de bestaande back-end|
|/Service/APIs/Read|Lijst met alle geregistreerde API's of Get details van de API|
|/Service/APIs/Write|Nieuwe API maken of bijwerken van bestaande API-details|
|/Service/APIs/DELETE|Verwijder de bestaande API|
|/Service/APIs/Policy/Read|Configuratiedetails van beleid voor API ophalen|
|/Service/APIs/Policy/Write|Configuratiedetails van beleid voor API instellen|
|/Service/APIs/Policy/DELETE|Verwijder voor beleidsconfiguratie van de API|
|/Service/APIs/Operations/Read|Ophalen van lijst met bewerkingen voor bestaande API of details van API-bewerking ophalen|
|/Service/APIs/Operations/Write|Nieuwe API-bewerkingen voor het maken of bijwerken van bestaande API-bewerking|
|/Service/APIs/Operations/DELETE|Verwijder de bestaande API-bewerking|
|/Service/APIs/Operations/Policy/Read|Configuratiedetails van beleid voor bewerking ophalen|
|/Service/APIs/Operations/Policy/Write|Configuratiedetails van beleid voor opnieuw instellen|
|/Service/APIs/Operations/Policy/DELETE|Voor beleidsconfiguratie van de bewerking verwijderen|
|/Service/Products/Read|Ophalen van lijst met producten of details van product ophalen|
|/Service/Products/Write|Nieuw product maken of bijwerken van bestaande Productgegevens|
|/Service/Products/DELETE|Verwijder bestaande product|
|/Service/Products/Subscriptions/Read|Lijst met abonnementen product ophalen|
|/Service/Products/APIs/Read|Haal de lijst met API's tooexisting product toegevoegd|
|/Service/Products/APIs/Write|Bestaande API tooexisting product toevoegen|
|/Service/Products/APIs/DELETE|Bestaande API verwijderen uit bestaande product|
|/Service/Products/Policy/Read|Voor beleidsconfiguratie van bestaande product ophalen|
|/Service/Products/Policy/Write|Stel de beleidsconfiguratie van voor bestaande product|
|/Service/Products/Policy/DELETE|Configuratie van beleid verwijderen uit bestaande product|
|/Service/Products/Groups/Read|Lijst met groepen van ontwikkelaars die zijn gekoppeld aan het product verkrijgen|
|/Service/Products/Groups/Write|Bestaande developer-groep koppelen aan bestaande product|
|/Service/Products/Groups/DELETE|Koppeling van bestaande developer-groep met bestaande product verwijderen|
|/Service/openidConnectProviders/Read|Lijst met providers OpenID Connect of details van OpenID Connect-Provider opvragen|
|/Service/openidConnectProviders/Write|Een nieuwe OpenID Connect-Provider of Update details van een bestaande OpenID Connect-Provider maken|
|/Service/openidConnectProviders/DELETE|Bestaande OpenID Connect Provider verwijderen|
|/Service/Certificates/Read|Ophalen van lijst met certificaten of details van een certificaat ophalen|
|/Service/Certificates/Write|Nieuw certificaat toevoegen|
|/Service/Certificates/DELETE|Verwijder bestaande certificaat|
|/Service/Properties/Read|Lijst van alle eigenschappen opgehaald of details van de opgegeven eigenschap opgehaald|
|/Service/Properties/Write|Een nieuwe eigenschap maken of bijwerken van waarde voor de opgegeven eigenschap|
|/Service/Properties/DELETE|Hiermee verwijdert u het bestaande eigenschap|
|/Service/Groups/Read|Lijst met groepen of informatie opgehaald van een groep|
|/Service/Groups/Write|Nieuwe groep maken of bijwerken van bestaande groepsnaam details|
|/Service/Groups/DELETE|Verwijder bestaande groep|
|/Service/Groups/Users/Read|Lijst van de groepsgebruikers ophalen|
|/Service/Groups/Users/Write|Bestaande tooexisting gebruikersgroep toevoegen|
|/Service/Groups/Users/DELETE|Bestaande gebruiker verwijderen uit bestaande groep|
|/Service/authorizationServers/Read|Ophalen van lijst met autorisatieservers of details van de autorisatie-server ophalen|
|/Service/authorizationServers/Write|Een nieuwe autorisatie-server of de details van de Update van een bestaande autorisatie-server maken|
|/Service/authorizationServers/DELETE|Verwijderen van bestaande autorisatie-server|
|/Service/Reports/bySubscription/Read|Rapport dat is samengevoegd per abonnement ophalen.|
|/Service/Reports/byRequest/Read|Rapportagegegevens van aanvragen|
|/Service/Reports/byOperation/Read|Rapport samenvoegen met de bewerkingen ophalen|
|/Service/Reports/byGeo/Read|Rapport samenvoegen met geografische regio ophalen|
|/Service/Reports/byUser/Read|Rapport geaggregeerd door ontwikkelaars ophalen.|
|/Service/Reports/byTime/Read|Rapport samenvoegen met perioden ophalen|
|/Service/Reports/byApi/Read|Rapport samenvoegen met API's ophalen|
|/Service/Reports/byProduct/Read|Rapport samenvoegen met producten ophalen.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Bewerking | Beschrijving |
|---|---|
|/ appidentities/lezen|Retourneert Hallo resource (website) geregistreerd bij Hallo Gateway.|
|/ appidentities/schrijven|Maakt een nieuwe App-id.|
|/ appidentities/verwijderen|Hiermee verwijdert u een bestaande App-identiteit.|
|/deploymenttemplates/listMetadata/Action|Een lijst met gebruikersinterface-metagegevens die zijn gekoppeld aan het Hallo-API-App-pakket.|
|/deploymenttemplates/Generate/Action|Retourneert een implementatiesjabloon tooprovision API-App-exemplaren.|
|/ gateways/lezen|Retourneert Hallo Gateway-exemplaren.|
|/ gateways/schrijven|Een nieuwe Gateway maken of bijwerken van bestaande.|
|/ gateways/verwijderen|Hiermee verwijdert u een bestaand gatewayexemplaar.|
|/gateways/listLoginUris/Action|Vult tokenopslag en retourneert OAuth-aanmelding URI's.|
|/gateways/listKeys/Action|Retourneert de geheimen van de Gateway.|
|/gateways/tokens/Write|Maakt een nieuw Zumo-Token met Hallo opgegeven naam.|
|/gateways/Registrations/Read|Retourneert Hallo resource (website) geregistreerd bij Hallo Gateway.|
|/gateways/Registrations/Write|Registreert een bron (web site) met Hallo Gateway.|
|/gateways/Registrations/DELETE|Heft de registratie van een resource (website) van Hallo Gateway.|
|/ apiapps/lezen|Retourneert Hallo API-App-exemplaar.|
|/ apiapps/schrijven|Een nieuwe API-App maken of bijwerken van bestaande.|
|/ apiapps/verwijderen|Hiermee verwijdert u een bestaand exemplaar van API-App.|
|/apiapps/listStatus/Action|Retourneert de status van de API-App.|
|/apiapps/listKeys/Action|API-App retourneert geheimen.|
|/apiapps/apidefinitions/Read|Retourneert de API-definitie-API-App.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Bewerking | Beschrijving |
|---|---|
|/ elevateAccess/actie|Verleent Hallo aanroeper toegang op tenantscope Hallo beheerder voor gebruikerstoegang|
|/classicAdministrators/Read|Hallo-beheerders voor Hallo abonnement leest.|
|classicAdministrators/schrijven|Toevoegen of wijzigen van de beheerder tooa abonnement.|
|/classicAdministrators/DELETE|Hallo beheerder verwijdert uit het Hallo-abonnement.|
|/locks/Read|Haalt de vergrendelingen bij Hallo opgegeven bereik.|
|vergrendelingen/schrijven|Hiermee worden vergrendelingen toegevoegd bij Hallo opgegeven bereik.|
|/locks/DELETE|Verwijder de vergrendelingen bij Hallo opgegeven bereik.|
|/policyAssignments/Read|Informatie ophalen over een beleidstoewijzing.|
|policyAssignments/schrijven|Maak een beleid voor toewijzing op Hallo opgegeven bereik.|
|/policyAssignments/DELETE|Verwijder een beleidstoewijzing op Hallo opgegeven bereik.|
|/permissions/Read|Geeft een lijst van alle Hallo machtigingen Hallo beller voor een bepaald bereik.|
|/roleDefinitions/Read|Informatie ophalen over een roldefinitie.|
|roleDefinitions/schrijven|Een aangepaste roldefinitie maken of bijwerken met opgegeven machtigingen of toewijsbare bereiken.|
|/roleDefinitions/DELETE|Verwijder Hallo opgegeven aangepaste roldefinitie.|
|/providerOperations/Read|Bewerkingen ophalen voor alle resourceproviders die kunnen worden gebruikt in roldefinities.|
|/policyDefinitions/Read|Informatie ophalen over een beleidsdefinitie.|
|policyDefinitions/schrijven|De definitie van een aangepast beleid maken.|
|/policyDefinitions/DELETE|Een beleidsdefinitie verwijderen.|
|/roleAssignments/Read|Informatie ophalen over een roltoewijzing.|
|roleAssignments/schrijven|Een gebruikersrol maakt toewijzing op Hallo opgegeven bereik.|
|/roleAssignments/DELETE|Een roltoewijzing bij Hallo verwijderen opgegeven bereik.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| Bewerking | Beschrijving |
|---|---|
|/automationAccounts/Read|Hiermee ontvangt u een Azure Automation-account|
|automationAccounts/schrijven|Maken of bijwerken van een Azure Automation-account|
|/automationAccounts/DELETE|Hiermee verwijdert u een Azure Automation-account|
|/automationAccounts/Configurations/readContent/Action|Hiermee wordt de inhoud van een Azure Automation DSC opgehaald|
|/automationAccounts/hybridRunbookWorkerGroups/Read|Resources voor de Hybrid Runbook Worker gelezen|
|/automationAccounts/hybridRunbookWorkerGroups/DELETE|Resources voor de Hybrid Runbook Worker worden verwijderd|
|/automationAccounts/jobSchedules/Read|Een Azure Automation-taakschema opgehaald|
|/automationAccounts/jobSchedules/Write|Hiermee maakt u een Azure Automation-taakschema|
|/automationAccounts/jobSchedules/DELETE|Hiermee wordt een Azure Automation-taakschema verwijderd|
|/automationAccounts/connectionTypes/Read|Een Azure Automation verbindingstype-asset opgehaald|
|/automationAccounts/connectionTypes/Write|Hiermee maakt u een Azure Automation verbindingstype-asset|
|/automationAccounts/connectionTypes/DELETE|Hiermee wordt een Azure Automation verbindingstype-asset verwijderd|
|/automationAccounts/modules/Read|Een Azure Automation-module opgehaald|
|/automationAccounts/modules/Write|Maken of bijwerken van een Azure Automation-module|
|/automationAccounts/modules/DELETE|Hiermee verwijdert u een Azure Automation-module|
|/automationAccounts/credentials/Read|Een Azure Automation-referentieasset opgehaald|
|/automationAccounts/credentials/Write|Maken of bijwerken van een Azure Automation-referentieasset|
|/automationAccounts/credentials/DELETE|Hiermee wordt een Azure Automation-referentieasset verwijderd|
|/automationAccounts/Certificates/Read|Een Azure Automation-certificaatasset opgehaald|
|/automationAccounts/Certificates/Write|Maken of bijwerken van een Azure Automation-certificaatactivum|
|/automationAccounts/Certificates/DELETE|Een Azure Automation-certificaatactivum verwijderen|
|/automationAccounts/Schedules/Read|Een Azure Automation-planningsasset opgehaald|
|/automationAccounts/Schedules/Write|Maken of bijwerken van een Azure Automation-planningsasset|
|/automationAccounts/Schedules/DELETE|Hiermee wordt een Azure Automation-planningsasset verwijderd|
|/automationAccounts/Jobs/Read|Een Azure Automation-taak opgehaald|
|/automationAccounts/Jobs/Write|Hiermee maakt u een Azure Automation-taak|
|/automationAccounts/Jobs/Stop/Action|Hiermee wordt een Azure Automation-taak gestopt|
|/automationAccounts/Jobs/Suspend/Action|Een Azure Automation-taak wordt onderbroken|
|/automationAccounts/Jobs/Resume/Action|Een Azure Automation-taak hervatten|
|/automationAccounts/Jobs/runbookContent/Action|Hallo-inhoud van hello Azure Automation-runbook opgehaald bij Hallo Hallo taakuitvoering|
|/automationAccounts/Jobs/output/Action|Hallo-uitvoer van een taak opgehaald|
|/automationAccounts/Jobs/Read|Een Azure Automation-taak opgehaald|
|/automationAccounts/Jobs/Write|Hiermee maakt u een Azure Automation-taak|
|/automationAccounts/Jobs/Stop/Action|Hiermee wordt een Azure Automation-taak gestopt|
|/automationAccounts/Jobs/Suspend/Action|Een Azure Automation-taak wordt onderbroken|
|/automationAccounts/Jobs/Resume/Action|Een Azure Automation-taak hervatten|
|/automationAccounts/Jobs/streams/Read|Een Azure Automation-taakstroom opgehaald|
|/automationAccounts/Connections/Read|Een Azure Automation-verbindingsasset opgehaald|
|/automationAccounts/Connections/Write|Maken of bijwerken van een Azure Automation-verbindingsasset|
|/automationAccounts/Connections/DELETE|Hiermee wordt een Azure Automation verbindingstype-asset verwijderd|
|/automationAccounts/Variables/Read|Hiermee wordt een variabel Azure Automation-asset gelezen|
|/automationAccounts/Variables/Write|Maken of bijwerken van een Azure Automation-variabelenactivum|
|/automationAccounts/Variables/DELETE|Hiermee wordt een variabel Azure Automation-asset verwijderd|
|/automationAccounts/runbooks/readContent/Action|Hallo-inhoud van een Azure Automation-runbook opgehaald|
|/automationAccounts/runbooks/Read|Een Azure Automation-runbook opgehaald|
|/automationAccounts/runbooks/Write|Maken of bijwerken van een Azure Automation-runbook|
|/automationAccounts/runbooks/DELETE|Hiermee verwijdert u een Azure Automation-runbook|
|/automationAccounts/runbooks/Draft/readContent/Action|Hallo-inhoud van een Azure Automation-runbookconcept opgehaald|
|/automationAccounts/runbooks/Draft/writeContent/Action|Hallo-inhoud van een Azure Automation-runbookconcept maken|
|/automationAccounts/runbooks/Draft/Read|Een Azure Automation-runbookconcept opgehaald|
|/automationAccounts/runbooks/Draft/Publish/Action|Een Azure Automation-runbookconcept gepubliceerd|
|/automationAccounts/runbooks/Draft/undoEdit/Action|Bewerkingen tooan Azure Automation-runbookconcept ongedaan maken|
|/automationAccounts/runbooks/Draft/testJob/Read|Een Azure Automation-runbookconcept opgehaald|
|/automationAccounts/runbooks/Draft/testJob/Write|Hiermee maakt u een Azure Automation-runbookconcept|
|/automationAccounts/runbooks/Draft/testJob/Stop/Action|Hiermee wordt een Azure Automation-runbookconcept gestopt|
|/automationAccounts/runbooks/Draft/testJob/Suspend/Action|Wordt een Azure Automation-runbookconcept onderbroken|
|/automationAccounts/runbooks/Draft/testJob/Resume/Action|Een Azure Automation-runbookconcept hervatten|
|/automationAccounts/webhooks/Read|Hiermee wordt een Azure Automation-webhook gelezen|
|/automationAccounts/webhooks/Write|Maken of bijwerken van een Azure Automation-webhook|
|/automationAccounts/webhooks/DELETE|Hiermee wordt een Azure Automation-webhook verwijderd |
|/automationAccounts/webhooks/generateUri/Action|Een URI voor een Azure Automation-webhook gegenereerd|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Deze provider is niet een volledige ARM-provider en biedt geen bewerkingen ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo-abonnement voor Hallo Batch Resource Provider registreert en Hiermee kunt u Hallo Batch-accounts maken|
|batchAccounts/schrijven|Een nieuwe Batch-account maken of bijwerken van een bestaande Batch-account|
|/batchAccounts/Read|Een lijst met Batch-accounts of Hallo eigenschappen van een Batch-account opgehaald|
|/batchAccounts/DELETE|Hiermee verwijdert u een Batch-account|
|/batchAccounts/listkeys/Action|Een lijst met sleutels voor een Batch-account toegang tot|
|/batchAccounts/regeneratekeys/Action|Opnieuw toegangssleutels voor een Batch-account|
|/batchAccounts/syncAutoStorageKeys/Action|Toegangstoetsen voor storage-account voor Hallo automatisch is geconfigureerd voor een Batch-account wordt gesynchroniseerd|
|/batchAccounts/Applications/Read|Eigenschappen van een toepassing hello opgehaald of ingesteld geeft een lijst van toepassingen|
|/batchAccounts/Applications/Write|Een nieuwe toepassing maken of bijwerken van een bestaande toepassing|
|/batchAccounts/Applications/DELETE|Een toepassing verwijderen|
|/batchAccounts/Applications/Versions/Read|Hallo-eigenschappen van een toepassingspakket opgehaald|
|/batchAccounts/Applications/Versions/Write|Een nieuw pakket maken of bijwerken van een bestaand toepassingspakket|
|/batchAccounts/Applications/Versions/Activate/Action|Hiermee activeert u een toepassingspakket|
|/batchAccounts/Applications/Versions/DELETE|Hiermee verwijdert u een toepassingspakket|
|/Locations/Quotas/Read|Batch-quota opgehaald Hallo opgegeven abonnement op Hallo opgegeven Azure-regio|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Bewerking | Beschrijving |
|---|---|
|/Invoices/Read|Een lijst met beschikbare facturen|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Bewerking | Beschrijving |
|---|---|
|/ mapApis/lezen|Leesbewerking|
|/ mapApis/schrijven|Schrijfbewerking|
|/ mapApis/verwijderen|Het verwijderen|
|/mapApis/regenerateKey/Action|Hallo sleutel wordt opnieuw gegenereerd|
|/mapApis/listSecrets/Action|Lijst Hallo geheimen|
|/mapApis/listSingleSignOnToken/Action|Hallo lezen eenmalige aanmelding op autorisatie Token voor Resource|
|Bewerkingen/leestijd|Beschrijving van het Hallo-bewerking.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Bewerking | Beschrijving |
|---|---|
|/ checknameavailability/actie|Controleert of een naam beschikbaar voor gebruik met een nieuwe Redis-Cache|
|registratie-/ actie|Hallo 'Microsoft.Cache' resourceprovider geregistreerd met een abonnement|
|/ unregister/actie|Heft de registratie van Hallo 'Microsoft.Cache' resourceprovider met een abonnement|
|redis/schrijven|Wijzig de instellingen en configuratie in de beheerportal Hallo Hallo Redis-Cache|
|/redis/Read|Instellingen en configuratie Hallo Redis-Cache weergeven in Hallo-beheerportal|
|/redis/DELETE|Delete Hallo volledige Redis-Cache|
|/redis/listKeys/Action|Weergave Hallo-waarde van de toegangssleutels voor Redis-Cache in Hallo-beheerportal|
|/redis/regenerateKey/Action|Hallo-waarde van de toegangssleutels voor Redis-Cache in de beheerportal Hallo wijzigen|
|/redis/import/Action|Gegevens met een opgegeven indeling in Redis importeren vanuit meerdere blobs|
|/redis/export/Action|Exporteren van gegevens tooprefixed storage-blobs in de opgegeven indeling Redis|
|/redis/forceReboot/Action|Een cache-instantie geforceerd opnieuw opstarten met mogelijk gegevensverlies.|
|/redis/Stop/Action|Stoppen van een cache-exemplaar.|
|/redis/start/Action|Start een cache-exemplaar.|
|/redis/metricDefinitions/Read|Hallo beschikbare metrische gegevens voor een Redis-Cache opgehaald|
|/redis/firewallRules/Read|Hallo IP-firewall-regels van een Redis-Cache ophalen|
|/redis/firewallRules/Write|Hallo IP-firewallregels van een Redis-Cache bewerken|
|/redis/firewallRules/DELETE|IP-firewallregels van een Redis-Cache verwijderen|
|/redis/listUpgradeNotifications/Read|Lijst Hallo nieuwste Upgrademeldingen weergeven voor de cachetenant Hallo.|
|/redis/linkedservers/Read|Gekoppelde Servers die zijn gekoppeld aan een redis-cache niet ophalen.|
|/redis/linkedservers/Write|Toevoegen van de gekoppelde Server tooa Redis-Cache|
|/redis/linkedservers/DELETE|Gekoppelde Server verwijderen uit een Redis-Cache|
|/redis/patchSchedules/Read|Hallo-opgehaald patching planning van een Redis-Cache|
|/redis/patchSchedules/Write|Hallo patchen planning van een Redis-Cache wijzigen|
|/redis/patchSchedules/DELETE|Hallo patch planning van een Redis-Cache verwijderen|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Bewerking | Beschrijving |
|---|---|
|/ provisionGlobalAppServicePrincipalInUserTenant/actie|Service-principal voor service-principal voor app inrichten|
|/ validateCertificateRegistrationInformation/actie|Aankoop certificaatobject valideren zonder deze te verzenden|
|registratie-/ actie|De registerbronprovider Hallo Microsoft Certificates voor Hallo-abonnement|
|/ certificateOrders/schrijven|Een nieuwe certificateOrder toevoegen of een bestaande bijgewerkt|
|/ certificateOrders/verwijderen|Een bestaande AppServiceCertificate verwijderen|
|/ certificateOrders/lezen|Hallo-lijst van CertificateOrders ophalen|
|/certificateOrders/reissue/Action|Geef een bestaande certificateorder|
|/certificateOrders/renew/Action|Een bestaande certificateorder vernieuwen|
|/certificateOrders/retrieveCertificateActions/Action|Hallo-lijst van acties van certificaat ophalen|
|/certificateOrders/retrieveEmailHistory/Action|Geschiedenis van de e-certificaat ophalen|
|/certificateOrders/resendEmail/Action|Certificaat-e-mail opnieuw verzenden|
|/certificateOrders/verifyDomainOwnership/Action|Domein verifiëren|
|/certificateOrders/resendRequestEmails/Action|Aanvraag e-mailberichten tooanother e-mailadres verzenden|
|/certificateOrders/resendRequestEmails/Action|Site zegel voor een uitgegeven certificaat van de App-Service ophalen|
|/certificateOrders/Certificates/Write|Toevoegen van een nieuw certificaat of een bestaande bijgewerkt|
|/certificateOrders/Certificates/DELETE|Een bestaand certificaat verwijderen|
|/certificateOrders/Certificates/Read|Hallo-lijst van certificaten ophalen|

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|TooClassic Compute registreren|
|/ checkDomainNameAvailability/actie|Controleert de beschikbaarheid Hallo van een bepaald domeinnaam.|
|/ moveSubscriptionResources/actie|Verplaats alle klassieke resources tooa ander abonnement.|
|/ validateSubscriptionMoveAvailability/actie|Valideren van het abonnement Hallo beschikbaarheid voor klassieke move-bewerking.|
|/operatingSystemFamilies/Read|Geeft een lijst van Hallo Gast besturingssystemen beschikbaar is in Microsoft Azure en vermeldt tevens Hallo besturingssysteemversies beschikbaar voor elke f
|/Capabilities/Read|Hallo mogelijkheden bevat|
|/operatingSystems/Read|Staan Hallo-versies van het gastbesturingssysteem Hallo die momenteel beschikbaar in Microsoft Azure zijn.|
|/resourceTypes/skus/Read|Haalt de Sku-lijst Hallo voor ondersteunde resourcetypen.|
|/domainNames/Read|Hallo domeinnamen voor resources retourneren.|
|domainNames/schrijven|Toevoegen of wijzigen van Hallo domeinnamen voor resources.|
|/domainNames/DELETE|Hallo domeinnamen voor resources verwijderen.|
|/domainNames/swap/Action|Wisselt Hallo sleuf toohello productiesite voor fasering.|
|/domainNames/serviceCertificates/Read|Retourneert Hallo servicecertificaten die worden gebruikt.|
|/domainNames/serviceCertificates/Write|Toevoegen of wijzigen van de gebruikte servicecertificaten Hallo.|
|/domainNames/serviceCertificates/DELETE|Hallo gebruikte servicecertificaten verwijderen.|
|/domainNames/serviceCertificates/operationStatuses/Read|Hallo bewerkingsstatus van servicecertificaten van domeinnamen van Hallo domein leest.|
|/domainNames/Capabilities/Read|Hier ziet u Hallo domein mogelijkheden voor domeinnaamgeving weer|
|/domainNames/Extensions/Read|Retourneert Hallo domeinnaamextensies.|
|/domainNames/Extensions/Write|Hallo domeinnaamextensies toevoegen.|
|/domainNames/Extensions/DELETE|Hallo domeinnaamextensies verwijderen.|
|/domainNames/Extensions/operationStatuses/Read|Leest Hallo bewerkingsstatus van domeinnaamextensies Hallo-domein.|
|/domainNames/Active/Write|Hiermee stelt u Hallo active domeinnaam.|
|/domainNames/slots/Read|Toont Hallo implementatiesites.|
|/domainNames/slots/Write|Gemaakt of bijgewerkt Hallo-implementatie.|
|/domainNames/slots/DELETE|Hiermee wordt een bepaald implementatiesleuf verwijderd.|
|/domainNames/slots/start/Action|Hiermee wordt een implementatiesleuf gestart.|
|/domainNames/slots/Stop/Action|Hallo implementatiesleuf onderbreekt.|
|/domainNames/slots/operationStatuses/Read|Hiermee Hallo bewerkingsstatus voor Hallo domein domeinnaamsleuven gelezen.|
|/domainNames/slots/roles/Read|Hallo-rol voor Hallo implementatiesleuf opgehaald.|
|/domainNames/slots/roles/extensionReferences/Read|Retourneert Hallo extensieverwijzing voor implementatiesiterol Hallo.|
|/domainNames/slots/roles/extensionReferences/Write|Toevoegen of wijzigen van Hallo extensieverwijzing voor implementatiesiterol Hallo.|
|/domainNames/slots/roles/extensionReferences/DELETE|Hallo extensieverwijzing voor implementatiesiterol Hallo verwijderen.|
|/domainNames/slots/roles/extensionReferences/operationStatuses/Read|De bewerkingsstatus Hallo voor Hallo domein namen sleuven rollen extensie verwijzingen leest.|
|/domainNames/slots/roles/roleInstances/Read|Hallo rolinstantie ophalen.|
|/domainNames/slots/roles/roleInstances/restart/Action|Rolinstanties opnieuw is opgestart.|
|/domainNames/slots/roles/roleInstances/reimage/Action|Reimages hello rolinstantie.|
|/domainNames/slots/roles/roleInstances/operationStatuses/Read|Hallo bewerkingsstatus van rolinstanties van Hallo domein namen sleuven rollen leest.|
|/domainNames/slots/State/start/Write|Wijzigingen Hallo implementatiesleuf status toostopped.|
|/domainNames/slots/State/Stop/Write|Wijzigingen Hallo implementatiesleuf status toostarted.|
|/domainNames/slots/upgradeDomain/Write|Helpt upgrade Hallo-domein.|
|/domainNames/internalLoadBalancers/Read|Hiermee haalt u Hallo interne load balancers.|
|/domainNames/internalLoadBalancers/Write|Hiermee wordt een nieuwe interne taakverdeling gemaakt.|
|/domainNames/internalLoadBalancers/DELETE|Een nieuwe interne taakverdeling verwijderen.|
|/domainNames/internalLoadBalancers/operationStatuses/Read|Leest de bewerkingsstatus van Hallo voor interne load balancers van Hallo domeinnamen.|
|/domainNames/loadBalancedEndpointSets/Read|Hallo taakverdeling eindpuntsets toont|
|/domainNames/loadBalancedEndpointSets/operationStatuses/Read|Leest de bewerkingsstatus van Hallo voor Hallo eindpuntsets van taakverdeling domeinnamen.|
|/domainNames/availabilitySets/Read|Hallo-beschikbaarheid instellen voor Hallo resource weergeven.|
|/Quotas/Read|Hallo-quotum voor Hallo abonnement niet ophalen.|
|/virtualMachines/Read|Hiermee wordt een lijst met virtuele machines opgehaald.|
|virtuele machines/schrijven|Hiermee worden virtuele machines toegevoegd of gewijzigd.|
|/virtualMachines/DELETE|Hiermee verwijdert u virtuele machines.|
|/virtualMachines/start/Action|Hallo virtuele machine te starten.|
|/virtualMachines/redeploy/Action|Redeploys hello virtuele machine.|
|/virtualMachines/restart/Action|Virtuele machines opnieuw is opgestart.|
|/virtualMachines/Stop/Action|Stopt Hallo virtuele machine.|
|/virtualMachines/Shutdown/Action|Afsluiten Hallo virtuele machine.|
|/virtualMachines/attachDisk/Action|Een virtuele machine voor gegevens schijf tooa koppelt.|
|/virtualMachines/detachDisk/Action|Hiermee wordt een gegevensschijf losgekoppeld van een virtuele machine.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/Action|Downloadt Hallo RDP-bestand voor de virtuele machine.|
|/virtualMachines/networkInterfaces /<br>associatedNetworkSecurityGroups leestijd|Hiermee wordt opgehaald die zijn gekoppeld aan de netwerkinterface Hallo Hallo netwerkbeveiligingsgroep.|
|/virtualMachines/networkInterfaces /<br>associatedNetworkSecurityGroups/schrijven|Voegt een netwerkbeveiligingsgroep Hallo netwerkinterface gekoppeld.|
|/virtualMachines/networkInterfaces /<br>associatedNetworkSecurityGroups/verwijderen|Hiermee verwijdert u Hallo netwerkbeveiligingsgroep Hallo netwerkinterface gekoppeld.|
|/virtualMachines/networkInterfaces /<br>operationStatuses associatedNetworkSecurityGroups leestijd|Leest de bewerkingsstatus Hallo voor Hallo virtuele machines die zijn gekoppeld netwerkbeveiligingsgroepen.|
|/virtualMachines/providers/Microsoft.Insights/metricDefinitions/Read|Hiermee haalt u Hallo metrische definities.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/Read|Hallo-instellingen voor diagnostische gegevens ophalen.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/Write|Hiermee worden diagnostische instellingen toegevoegd of gewijzigd.|
|/virtualMachines/metrics/Read|Hallo metrische gegevens opgehaald.|
|/virtualMachines/operationStatuses/Read|Hiermee Hallo bewerkingsstatus voor Hallo virtuele machines gelezen.|
|/virtualMachines/Extensions/Read|Hiermee wordt de extensie van de virtuele machine Hallo opgehaald.|
|/virtualMachines/Extensions/Write|De extensie van de virtuele machine Hallo plaatst.|
|/virtualMachines/Extensions/operationStatuses/Read|Hallo bewerkingsstatus van extensies van Hallo virtuele machines worden gelezen.|
|/virtualMachines/asyncOperations/Read|Hallo mogelijk asynchrone bewerkingen opgehaald|
|/virtualMachines/Disks/Read|Hiermee wordt een lijst met gegevensschijven opgehaald|
|/virtualMachines/associatedNetworkSecurityGroups/Read|Hiermee haalt u Hallo netwerkbeveiligingsgroep Hallo virtuele machine gekoppeld.|
|/virtualMachines/associatedNetworkSecurityGroups/Write|Voegt een netwerkbeveiligingsgroep Hallo virtuele machine gekoppeld.|
|/virtualMachines/associatedNetworkSecurityGroups/DELETE|Hiermee verwijdert u Hallo netwerkbeveiligingsgroep Hallo virtuele machine gekoppeld.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/Read|Leest de bewerkingsstatus Hallo voor Hallo virtuele machines die zijn gekoppeld netwerkbeveiligingsgroepen.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|TooClassic netwerk registreren|
|/gatewaySupportedDevices/Read|Hallo-lijst met ondersteunde apparaten opgehaald.|
|/reservedIps/Read|Opgehaald Hallo gereserveerde IP-adressen|
|reservedip/schrijven|Een nieuw gereserveerd IP toevoegen|
|/reservedIps/DELETE|Hiermee wordt een gereserveerd IP verwijderd.|
|/reservedIps/link/Action|Een gereserveerde IP koppelen|
|/reservedIps/join/Action|Deelnemen aan een gereserveerde IP|
|/reservedIps/operationStatuses/Read|Leest de bewerkingsstatus Hallo voor Hallo gereserveerd IP-adressen.|
|/virtualNetworks/Read|Hallo virtueel netwerk ophalen.|
|virtualNetworks/schrijven|Een nieuw virtueel netwerk wordt toegevoegd.|
|/virtualNetworks/DELETE|Hiermee verwijdert u het virtuele netwerk Hallo.|
|/virtualNetworks/peer/Action|Hiermee wordt een virtueel netwerk via peercommunicatie gebruikt met een ander virtueel netwerk.|
|/virtualNetworks/join/Action|Het virtuele netwerk Hallo koppelt.|
|/virtualNetworks/checkIPAddressAvailability/Action|Controleert de beschikbaarheid Hallo van een opgegeven IP-adres in een virtueel netwerk.|
|/virtualNetworks/Capabilities/Read|Hallo mogelijkheden bevat|
|/virtualNetworks/subnetten /<br>associatedNetworkSecurityGroups leestijd|Hiermee haalt u Hallo netwerkbeveiligingsgroep Hallo subnet gekoppeld.|
|/virtualNetworks/subnetten /<br>associatedNetworkSecurityGroups/schrijven|Voegt een netwerkbeveiligingsgroep Hallo subnet gekoppeld.|
|/virtualNetworks/subnetten /<br>associatedNetworkSecurityGroups/verwijderen|Hiermee verwijdert u Hallo netwerkbeveiligingsgroep Hallo subnet gekoppeld.|
|/virtualNetworks/subnetten /<br>operationStatuses associatedNetworkSecurityGroups leestijd|Hiermee kunt u de bewerkingsstatus Hallo van Hallo virtueel netwerk subnet netwerkbeveiligingsgroep gelezen.|
|/virtualNetworks/operationStatuses/Read|Hallo bewerkingsstatus van virtuele netwerken Hallo leest.|
|/virtualNetworks/gateways/Read|Hiermee wordt de virtuele netwerkgateways Hallo opgehaald.|
|/virtualNetworks/gateways/Write|Een gateway voor het virtuele netwerk wordt toegevoegd.|
|/virtualNetworks/gateways/DELETE|Hiermee verwijdert u de virtuele netwerkgateway Hallo.|
|/virtualNetworks/gateways/startDiagnostics/Action|Diagnostische test voor de virtuele netwerkgateway Hallo begint.|
|/virtualNetworks/gateways/stopDiagnostics/Action|Stopt de Hallo diagnostische test voor de virtuele netwerkgateway Hallo.|
|/virtualNetworks/gateways/downloadDiagnostics/Action|Hallo gateway diagnostics downloadt.|
|/virtualNetworks/gateways/listCircuitServiceKey/Action|Hallo circuitservicesleutel opgehaald.|
|/virtualNetworks/gateways/downloadDeviceConfigurationScript/Action|Hallo apparaatconfiguratiescript downloadt.|
|/virtualNetworks/gateways/listPackage/Action|Gatewaypakket voor een lijst met Hallo virtuele netwerk.|
|/virtualNetworks/gateways/operationStatuses/Read|Hallo bewerkingsstatus van de virtuele netwerkgateways Hallo leest.|
|/virtualNetworks/gateways/Packages/Read|Het gatewaypakket voor virtueel netwerk Hallo opgehaald.|
|/virtualNetworks/gateways/Connections/Read|Hallo-lijst met verbindingen opgehaald.|
|/virtualNetworks/gateways/Connections/Connect/Action|Verbinding van een site toosite gateway-verbinding.|
|/virtualNetworks/gateways/Connections/Disconnect/Action|Een site toosite gateway-verbinding wordt verbroken.|
|/virtualNetworks/gateways/Connections/test/Action|Een site toosite gateway-verbinding wordt getest.|
|/virtualNetworks/gateways/clientRevokedCertificates/Read|Lees Hallo ingetrokken clientcertificaten.|
|/virtualNetworks/gateways/clientRevokedCertificates/Write|Hiermee wordt een clientcertificaat ingetrokken.|
|/virtualNetworks/gateways/clientRevokedCertificates/DELETE|Hiermee wordt de intrekking van een clientcertificaat ongedaan gemaakt.|
|/virtualNetworks/gateways/clientRootCertificates/Read|Hallo client basiscertificaten zoeken.|
|/virtualNetworks/gateways/clientRootCertificates/Write|Hiermee wordt een nieuw clienthoofdcertificaat geüpload.|
|/virtualNetworks/gateways/clientRootCertificates/DELETE|Hiermee verwijdert u Hallo virtueel netwerk gateway clientcertificaat.|
|/virtualNetworks/gateways/clientRootCertificates/Download/Action|Hiermee wordt een certificaat gedownload op basis van miniatuur.|
|/virtualNetworks/gateways/clientRootCertificates/listPackage/Action|Gateway-certificaat voor virtueel netwerk op Hallo pakket bevat.|
|/networkSecurityGroups/Read|Hallo netwerkbeveiligingsgroep opgehaald.|
|networkSecurityGroups/schrijven|Hiermee wordt een nieuwe netwerkbeveiligingsgroep toegevoegd.|
|/networkSecurityGroups/DELETE|Hallo netwerkbeveiligingsgroep verwijderen|
|/networkSecurityGroups/operationStatuses/Read|Hiermee kunt u de bewerkingsstatus Hallo van Hallo netwerkbeveiligingsgroep gelezen.|
|/networkSecurityGroups/securityRules/Read|De beveiligingsregel Hallo opgehaald.|
|/networkSecurityGroups/securityRules/Write|Hiermee wordt een beveiligingsregel toegevoegd of bijgewerkt.|
|/networkSecurityGroups/securityRules/DELETE|Hiermee verwijdert u de beveiligingsregel Hallo.|
|/networkSecurityGroups/securityRules/operationStatuses/Read|De bewerkingsstatus Hallo van Hallo netwerkbeveiligingsregels leest.|
|/Quotas/Read|Hallo-quotum voor Hallo abonnement niet ophalen.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|TooClassic opslag registreren|
|/ checkStorageAccountAvailability/actie|Controleert op Hallo beschikbaarheid van een opslagaccount.|
|/Capabilities/Read|Hallo mogelijkheden bevat|
|/publicImages/Read|Installatiekopie van de openbare virtuele machine Hallo opgehaald.|
|/images/Read|Retourneert Hallo afbeelding.|
|/storageAccounts/Read|Hallo storage-account met opgegeven account Hallo retourneren.|
|storageAccounts/schrijven|Hiermee wordt een nieuw opslagaccount toegevoegd.|
|/storageAccounts/DELETE|Hallo storage-account verwijderen.|
|/storageAccounts/listKeys/Action|Geeft een lijst Hallo toegangstoetsen voor Hallo storage-accounts.|
|/storageAccounts/regenerateKey/Action|Genereert Hallo bestaande sneltoetsen voor Hallo storage-account.|
|/storageAccounts/operationStatuses/Read|Hallo bewerkingsstatus voor Hallo resource leest.|
|/storageAccounts/images/Read|Retourneert Hallo installatiekopie van het opslagaccount.|
|/storageAccounts/images/DELETE|Hiermee wordt de betreffende installatiekopie van het opslagaccount verwijderd.|
|/storageAccounts/Disks/Read|Retourneert Hallo opslagschijf-account.|
|/storageAccounts/Disks/Write|Hiermee wordt een opslagaccountschijf toegevoegd.|
|/storageAccounts/Disks/DELETE|Hiermee wordt een opgegeven opslagaccountschijf verwijderd.|
|/storageAccounts/Disks/operationStatuses/Read|Hallo bewerkingsstatus voor Hallo resource leest.|
|/storageAccounts/osImages/Read|Retourneert Hallo besturingssysteemkopie van opslag.|
|/storageAccounts/osImages/DELETE|Hiermee wordt de betreffende installatiekopie van het besturingssysteem van een opslagaccount verwijderd.|
|/storageAccounts/Services/Read|Hallo beschikbare services worden opgehaald.|
|/storageAccounts/Services/metricDefinitions/Read|Hiermee haalt u Hallo metrische definities.|
|/storageAccounts/Services/metrics/Read|Hallo metrische gegevens opgehaald.|
|/storageAccounts/Services/diagnosticSettings/Read|Hallo-instellingen voor diagnostische gegevens ophalen.|
|/storageAccounts/Services/diagnosticSettings/Write|Hiermee worden diagnostische instellingen toegevoegd of gewijzigd.|
|/Disks/Read|Retourneert Hallo opslagschijf-account.|
|/osImages/Read|Retourneert Hallo installatiekopie.|
|/Quotas/Read|Hallo-quotum voor Hallo abonnement niet ophalen.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Bewerking | Beschrijving |
|---|---|
|/Accounts/read|API-accounts worden gelezen.|
|accounts/schrijven|Schrijft API-Accounts.|
|/accounts/DELETE|Hiermee verwijdert u de API-accounts|
|/accounts/listKeys/Action|Lijst met sleutels|
|/accounts/regenerateKey/Action|Sleutel opnieuw genereren|
|/accounts/skus/Read|Beschikbare SKU's voor een bestaande resource leest.|
|/accounts/usages/Read|Hallo quotagebruik voor een bestaande resource niet ophalen.|
|Bewerkingen/leestijd|Beschrijving van het Hallo-bewerking.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Bewerking | Beschrijving |
|---|---|
|RateCard/leestijd|Retourneert bieden gegevens, metagegevens van de resource/meter en tarieven voor Hallo opgegeven abonnement.|
|UsageAggregates/leestijd|Haalt de Microsoft Azure verbruik door een abonnement. Hallo resultaat bevat statistische gegevens over het gebruik, abonnement en de resource verwante gegevens, op een bepaalde periode.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hiermee wordt het abonnement bij de Microsoft.Compute-resourceprovider geregistreerd|
|/restorePointCollections/Read|Hallo-eigenschappen van een verzameling restore-punt opgehaald|
|restorePointCollections/schrijven|Maakt een nieuwe verzameling van de restore-punt of een bestaande bijgewerkt|
|/restorePointCollections/DELETE|Hiermee verwijdert u Hallo terugzetten punt verzameling en opgenomen herstelpunten|
|/restorePointCollections/restorePoints/Read|Hallo-eigenschappen van een herstelpunt opgehaald|
|/restorePointCollections/restorePoints/Write|Een nieuw herstelpunt wordt gemaakt|
|/restorePointCollections/restorePoints/DELETE|Hiermee verwijdert u het herstelpunt Hallo|
|/restorePointCollections/restorePoints/retrieveSasUris/Action|Hallo-eigenschappen van een herstelpunt samen met de blob-SAS URI's ophalen|
|/virtualMachineScaleSets/Read|Hallo-eigenschappen van een virtuele-machineschaalset opgehaald|
|virtualMachineScaleSets/schrijven|Hiermee wordt een nieuwe virtuele-machineschaalset gemaakt of een bestaande bijgewerkt|
|/virtualMachineScaleSets/DELETE|Hallo virtuele-machineschaalset verwijderen|
|/virtualMachineScaleSets/start/Action|Start Hallo exemplaren van Hallo virtuele-machineschaalset|
|/virtualMachineScaleSets/powerOff/Action|Bevoegdheden uit Hallo exemplaren van Hallo virtuele-machineschaalset|
|/virtualMachineScaleSets/restart/Action|Hallo-exemplaren van Hallo virtuele-machineschaalset opnieuw wordt opgestart|
|/virtualMachineScaleSets/deallocate/Action|Schaalset uitgeschakeld en releases Hallo rekenresources voor Hallo exemplaren van Hallo virtuele-machineschaalset |
|/virtualMachineScaleSets/manualUpgrade/Action|Handmatig updates exemplaren toolatest model van Hallo virtuele-machineschaalset|
|/virtualMachineScaleSets/Scale/Action|Schalen / uitschalen aantal exemplaren van een bestaande virtuele-machineschaalset instellen|
|/virtualMachineScaleSets/instanceView/Read|Hallo instantieweergave van Hallo virtuele-machineschaalset opgehaald|
|/virtualMachineScaleSets/skus/Read|Een lijst met Hallo geldige SKU's voor een bestaande virtuele-machineschaalset|
|/virtualMachineScaleSets/virtualMachines/Read|Hallo-eigenschappen van een virtuele Machine in een VM-Schaalset opgehaald|
|/virtualMachineScaleSets/virtualMachines/DELETE|Een specifieke virtuele machine uit een VM-schaalset verwijderen.|
|/virtualMachineScaleSets/virtualMachines/start/Action|Hiermee wordt de instantie van een specifieke virtuele machine in een VM-schaalset gestart.|
|/virtualMachineScaleSets/virtualMachines/powerOff/Action|Hiermee wordt de instantie van een specifieke virtuele machine in een VM-schaalset uitgeschakeld.|
|/virtualMachineScaleSets/virtualMachines/restart/Action|Hiermee wordt de instantie van een specifieke virtuele machine in een VM-schaalset opnieuw gestart.|
|/virtualMachineScaleSets/virtualMachines/deallocate/Action|Schaalset uitgeschakeld en releases Hallo rekenresources voor een virtuele Machine in een VM-Schaalset.|
|/virtualMachineScaleSets/virtualMachines/instanceView/Read|Hallo instantieweergave van een virtuele Machine in een VM-Schaalset opgehaald.|
|/images/Read|Hallo-eigenschappen van installatiekopie Hallo opgehaald|
|installatiekopieën van/schrijven|Een nieuwe installatiekopie gemaakt of een bestaande bijgewerkt|
|/images/DELETE|Hiermee wordt de installatiekopie Hallo verwijderd|
|/Operations/Read|Hiermee wordt een lijst met bewerkingen weergegeven die beschikbaar zijn op de Microsoft.Compute-resourceprovider|
|/Disks/Read|Hallo-eigenschappen van een schijf opgehaald|
|schijven/schrijven|Hiermee wordt een nieuwe schijf gemaakt of een bestaande bijgewerkt|
|/Disks/DELETE|Hiermee verwijdert u Hallo schijf|
|/Disks/beginGetAccess/Action|Hallo SAS-URI van Hallo schijf ophalen voor blob-toegang|
|/Disks/endGetAccess/Action|Hallo SAS-URI van Hallo schijf intrekken|
|/Snapshots/Read|Hallo-eigenschappen van een momentopname opgehaald|
|momentopnamen van/schrijven|Hiermee wordt een nieuwe momentopname gemaakt of een bestaande bijgewerkt|
|/Snapshots/DELETE|Hiermee wordt een momentopname verwijderd|
|/availabilitySets/Read|Hallo-eigenschappen van een beschikbaarheidsset opgehaald|
|/ availabilitySets/schrijven|Hiermee wordt een nieuwe beschikbaarheidsset gemaakt of een bestaande bijgewerkt|
|/availabilitySets/DELETE|Hiermee verwijdert u de beschikbaarheidsset Hallo|
|/availabilitySets/vmSizes/Read|Lijst met beschikbare grootten voor het maken of bijwerken van een virtuele machine in de beschikbaarheidsset Hallo|
|/virtualMachines/Read|Hallo-eigenschappen van een virtuele machine ophalen|
|virtuele machines/schrijven|Hiermee wordt een nieuwe virtuele machine gemaakt of een bestaande bijgewerkt|
|/virtualMachines/DELETE|Hallo virtuele machine wordt verwijderd|
|/virtualMachines/start/Action|Start Hallo virtuele machine|
|/virtualMachines/powerOff/Action|Bevoegdheden Hallo virtuele machine uit. Houd er rekening mee dat de virtuele machine Hallo blijft toobe kosten in rekening gebracht.|
|/virtualMachines/redeploy/Action|Virtuele machine redeploys|
|/virtualMachines/restart/Action|Hallo virtuele machine opnieuw is opgestart|
|/virtualMachines/deallocate/Action|Bevoegdheden Hallo virtuele machine en releases Hallo uit berekenen bronnen|
|/virtualMachines/generalize/Action|Hallo virtuele machine staat tooGeneralized ingesteld en wordt Hallo virtuele machine voorbereid voor vastleggen|
|/virtualMachines/Capture/Action|Hallo virtuele machine vastgelegd door het kopiëren van virtuele harde schijven en wordt een sjabloon die gebruikte toocreate soortgelijke virtuele machines kan worden gegenereerd|
|/virtualMachines/convertToManagedDisks/Action|Hallo blobs gebaseerde schijven van de schijven voor virtuele machine toomanaged Hallo converteert|
|/virtualMachines/vmSizes/Read|Een lijst met beschikbare grootten Hallo virtuele machine kan worden bijgewerkt|
|/virtualMachines/instanceView/Read|Opgehaald Hallo gedetailleerde runtimestatus van Hallo virtuele machine en de bijbehorende bronnen|
|/virtualMachines/Extensions/Read|Hallo-eigenschappen van de extensie van een virtuele machine opgehaald|
|/virtualMachines/Extensions/Write|Hiermee wordt een nieuwe extensie van een virtuele machine gemaakt of een bestaande extensie bijgewerkt|
|/virtualMachines/Extensions/DELETE|Hiermee verwijdert u de extensie van de virtuele machine Hallo|
|/Locations/vmSizes/Read|Hiermee wordt een lijst weergegeven met de beschikbare grootten van virtuele machines op een locatie|
|/Locations/usages/Read|Servicelimieten en huidige gebruikshoeveelheden opgehaald voor de rekenresources Hallo-abonnement op een locatie|
|/Locations/Operations/Read|Hallo-status van een asynchrone bewerking opgehaald|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo-abonnement voor Hallo container register resourceprovider registreert en Hiermee kunt u container registers Hallo maken.|
|/checknameavailability/Read|Controleert die registernaam geldig is en niet wordt gebruikt.|
|/registries/Read|Retourneert de lijst met container registers Hallo of opgehaald Hallo eigenschappen voor Hallo opgegeven container register.|
|registers/schrijven|Maakt een register container met de opgegeven parameters Hallo of bij te werken Hallo eigenschappen of labels voor Hallo opgegeven container register.|
|/registries/DELETE|Hiermee verwijdert u een bestaande container-register.|
|/registries/listCredentials/Action|Hallo-aanmeldingsreferenties voor Hallo opgegeven container register bevat.|
|/registries/regenerateCredential/Action|Hallo-aanmeldingsreferenties voor Hallo opgegeven container register genereert.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Bewerking | Beschrijving |
|---|---|
|/containerServices/Subscriptions/Read|Get Hallo opgegeven Containerservices op basis van abonnement|
|/containerServices/resourceGroups/Read|Get Hallo opgegeven Containerservices op basis van resourcegroep|
|/containerServices/resourceGroups/ContainerServiceName/Read|Hallo opgehaald opgegeven Container Service|
|/containerServices/resourceGroups/ContainerServiceName/Write|Puts of Updates Hallo opgegeven Container Service|
|/containerServices/resourceGroups/ContainerServiceName/DELETE|Hiermee verwijdert u Hallo opgegeven Container Service|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Bewerking | Beschrijving |
|---|---|
|/ updateCommunicationPreference/actie|Communicatievoorkeur bijwerken|
|/ listCommunicationPreference/actie|Lijst communicatievoorkeur|
|/Applications/Read|Leesbewerking|
|/ applications/schrijven|Schrijfbewerking|
|/ applications/schrijven|Schrijfbewerking|
|/Applications/DELETE|Het verwijderen|
|/Applications/listSecrets/Action|Lijst met geheimen|
|/Applications/listSingleSignOnToken/Action|Eenmalige aanmelding Tokens lezen|
|/Operations/Read|leesbewerkingen|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Bewerking | Beschrijving |
|---|---|
|/hubs/Read|Een Azure klant Insights Hub lezen|
|hubs/schrijven|Maken of bijwerken van een Azure klant Insights Hub|
|/hubs/DELETE|Verwijderen van een Azure klant Insights Hub|
|/hubs/providers/Microsoft.Insights/metricDefinitions/Read|Hallo beschikbare metrische gegevens voor de resource opgehaald|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/Read|Hallo diagnostische instelling voor Hallo-resource opgehaald|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/Write|Maken of bijwerken van diagnostische instelling voor de resource Hallo Hallo|
|/hubs/providers/Microsoft.Insights/logDefinitions/Read|Hallo beschikbare logboeken opgehaald voor resource|
|/hubs/authorizationPolicies/Read|Geen inzichten Azure klant gedeeld toegangsbeleid handtekening lezen|
|/hubs/authorizationPolicies/Write|Een Azure klant Insights Shared Access Signature beleid maken of bijwerken|
|/hubs/authorizationPolicies/DELETE|Een Azure klant Insights Shared Access Signature-beleid verwijderen|
|/hubs/authorizationPolicies/regeneratePrimaryKey/Action|Azure klant Insights handtekening beleid voor gedeelde toegang primaire sleutel opnieuw genereren|
|/hubs/authorizationPolicies/regenerateSecondaryKey/Action|Azure klant Insights handtekening beleid voor gedeelde toegang secundaire sleutel opnieuw genereren|
|/hubs/Profiles/Read|Een Azure klant Insights profiel lezen|
|/hubs/Profiles/Write|Schrijven van een Azure klant Insights-profiel|
|/hubs/KPI/Read|Een Azure klant Insights Key Performance Indicator lezen|
|/hubs/KPI/Write|Maken of bijwerken van een Azure klant Insights Key Performance Indicator|
|/hubs/KPI/DELETE|Een Azure klant Insights Key Performance Indicator verwijderen|
|/hubs/Views/Read|Elke weergave Azure klant Insights-App lezen|
|/hubs/Views/Write|Maken of bijwerken van een Azure klant Insights App weergeven|
|/hubs/Views/DELETE|Elke klant Azure Insights App weergave verwijderen|
|/hubs/interactions/Read|Elke klant Azure Insights interactie lezen|
|/hubs/interactions/Write|Maken of bijwerken van elke klant Azure Insights interactie|
|/hubs/roleAssignments/Read|Lezen van een Azure klant Insights Rbac-toewijzing|
|/hubs/roleAssignments/Write|Maken of bijwerken van een Azure klant Insights Rbac-toewijzing|
|/hubs/roleAssignments/DELETE|Verwijderen van een Azure klant Insights Rbac-toewijzing|
|/hubs/connectors/Read|Lezen van een Azure klant Insights-Connector|
|/hubs/connectors/Write|Maken of bijwerken van een Azure klant Insights-Connector|
|/hubs/connectors/DELETE|Elke klant Azure Insights-Connector verwijderen|
|/hubs/connectors/mappings/Read|Lezen van een toewijzing van Azure klant Insights-Connector|
|/hubs/connectors/mappings/Write|Maken of bijwerken van een toewijzing van Azure klant Insights-Connector|
|/hubs/connectors/mappings/DELETE|Een toewijzing van Azure klant Insights-Connector verwijderen|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Bewerking | Beschrijving |
|---|---|
|/ checkNameAvailability/actie|Controleert de beschikbaarheid van de catalogus-naam voor de tenant.|
|/Catalogs/Read|Eigenschappen voor catalogi onder het abonnement of resourcegroep worden opgehaald.|
|catalogussen/schrijven|Catalogus of updates Hallo-labels en eigenschappen voor Hallo catalogus maakt.|
|/Catalogs/DELETE|Hiermee verwijdert u Hallo-catalogus.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| Bewerking | Beschrijving |
|---|---|
|/datafactories/Read|Data Factory leest.|
|datafactories/schrijven|Maken of bijwerken van de Data Factory|
|/datafactories/DELETE|Hiermee verwijdert u Data Factory.|
|/datafactories/datapipelines/Read|Leest de pijplijn.|
|/datafactories/datapipelines/DELETE|Hiermee verwijdert u een pijplijn.|
|/datafactories/datapipelines/pause/Action|De pijplijn wordt onderbroken.|
|/datafactories/datapipelines/Resume/Action|De pijplijn wordt hervat.|
|/datafactories/datapipelines/update/Action|Pijplijn van updates.|
|/datafactories/datapipelines/Write|Maken of bijwerken van de pijplijn|
|/datafactories/linkedServices/Read|Leest de gekoppelde service.|
|/datafactories/linkedServices/DELETE|Hiermee verwijdert u een gekoppelde service.|
|/datafactories/linkedServices/Write|Maken of bijwerken gekoppelde service|
|/datafactories/Tables/Read|Tabel leest.|
|/datafactories/Tables/DELETE|Hiermee verwijdert u een tabel.|
|/datafactories/Tables/Write|Maken of bijwerken|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Bewerking | Beschrijving |
|---|---|
|/Accounts/read|Informatie ophalen over Hallo DataLakeAnalytics-account.|
|accounts/schrijven|Account maken of bijwerken Hallo DataLakeAnalytics.|
|/accounts/DELETE|Hallo DataLakeAnalytics account verwijderen.|
|/accounts/firewallRules/Read|Informatie ophalen over een firewallregel.|
|/accounts/firewallRules/Write|Maken of bijwerken van een firewallregel.|
|/accounts/firewallRules/DELETE|Een firewallregel verwijderen.|
|/accounts/storageAccounts/Read|Gekoppelde Storage-account voor Hallo DataLakeAnalytics account niet ophalen.|
|/accounts/storageAccounts/Write|Een Storage account toohello DataLakeAnalytics account koppelen.|
|/accounts/storageAccounts/DELETE|Ontkoppelen van een opslagaccount van Hallo DataLakeAnalytics-account.|
|/accounts/storageAccounts/containers/Read|Containers onder Hallo Storage-account ophalen|
|/accounts/storageAccounts/containers/listSasTokens/Action|Lijst met SAS-Tokens voor Hallo Storage-container|
|/accounts/dataLakeStoreAccounts/Read|Gekoppelde DataLakeStore-account voor Hallo DataLakeAnalytics account niet ophalen.|
|/accounts/dataLakeStoreAccounts/Write|Een DataLakeStore account toohello DataLakeAnalytics account koppelen.|
|/accounts/dataLakeStoreAccounts/DELETE|Ontkoppelen van een account DataLakeStore van Hallo DataLakeAnalytics-account.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Bewerking | Beschrijving |
|---|---|
|/Accounts/read|Informatie ophalen over een bestaand DataLakeStore-account.|
|accounts/schrijven|Een nieuw DataLakeStore-account maken of bijwerken van een bestaand DataLakeStore-account.|
|/accounts/DELETE|Een bestaand DataLakeStore-account verwijderen.|
|/accounts/firewallRules/Read|Informatie ophalen over een firewallregel.|
|/accounts/firewallRules/Write|Maken of bijwerken van een firewallregel.|
|/accounts/firewallRules/DELETE|Een firewallregel verwijderen.|
|/accounts/trustedIdProviders/Read|Informatie ophalen over een vertrouwde id-provider.|
|/accounts/trustedIdProviders/Write|Maken of bijwerken van een vertrouwde id-provider.|
|/accounts/trustedIdProviders/DELETE|Verwijderen van een vertrouwde id-provider.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo-abonnement voor Hallo IotHub resource provider en schakelt Hallo maken van IotHub resources registreren|
|/ checkNameAvailability/actie|Controleer als IotHub naam beschikbaar is|
|Gebruik/lezen|Neem abonnement informatie over het gebruik voor deze provider.|
|/ operations/lezen|Alle bewerkingen van de ResourceProvider ophalen|
|/ iotHubs/lezen|Hallo IotHub resources opgehaald|
|/ iotHubs/schrijven|Maken of bijwerken van de IotHub-bron|
|/ iotHubs/verwijderen|IotHub-bron verwijderen|
|/iotHubs/listkeys/Action|Alle IotHub-sleutels ophalen|
|/iotHubs/exportDevices/Action|Exporteren van apparaten|
|/iotHubs/importDevices/Action|Apparaten importeren|
|IotHubs/metricDefinitions/leestijd|Hallo beschikbare metrische gegevens voor Hallo IotHub-service opgehaald|
|/iotHubs/iotHubKeys/listkeys/Action|IotHub Key voor Hallo gegeven naam ophalen|
|/iotHubs/iotHubStats/Read|IotHub-statistieken opvragen|
|/iotHubs/quotaMetrics/Read|Quotum metrische gegevens ophalen|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|EventHub Consumergroep maken|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|EventHub Consumer groep(en) ophalen|
|/iotHubs/eventHubEndpoints/consumerGroups/DELETE|EventHub Consumer-groep verwijderen|
|/iotHubs/Routing/routes/$ MATLAB/actie|Een bericht met alle bestaande Routes testen|
|/iotHubs/Routing/routes/$ testnew/actie|Een bericht met een opgegeven test Route testen|
|IotHubs/diagnosticSettings/leestijd|Hallo diagnostische instelling voor Hallo-resource opgehaald|
|/ IotHubs/diagnosticSettings/schrijven|Maken of bijwerken van diagnostische instelling voor de resource Hallo Hallo|
|/iotHubs/skus/Read|Geldige IotHub Skus ophalen|
|/iotHubs/Jobs/Read|Details van ingediend op gegeven IotHub taken ophalen|
|/iotHubs/routingEndpointsHealth/Read|Hallo-status van alle routering eindpunten voor een IotHub opgehaald|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Bewerking | Beschrijving |
|---|---|
|/ Abonnement/registreren/actie|Registreert de Hallo-abonnement|
|/Labs/DELETE|Labs verwijderen.|
|/Labs/Read|Labs lezen.|
|labs/schrijven|Toevoegen of wijzigen van labs.|
|/Labs/ListVhds/Action|Lijst van installatiekopieën van de schijven beschikbaar zijn voor het maken van aangepaste installatiekopie.|
|/Labs/GenerateUploadUri/Action|Een URI genereren voor het uploaden van aangepaste schijf installatiekopieën tooa Lab.|
|/Labs/CreateEnvironment/Action|Virtuele machines maken in een testomgeving.|
|/Labs/ClaimAnyVm/Action|Een willekeurige claimable virtuele machine in de testomgeving Hallo claimen.|
|/Labs/ExportResourceUsage/Action|Uitvoer Hallo lab Resourcegebruik in een opslagaccount|
|/Labs/Users/DELETE|Gebruikersprofielen verwijderen.|
|/Labs/Users/Read|Gebruikersprofielen worden gelezen.|
|/Labs/Users/Write|Toevoegen of wijzigen van gebruikersprofielen.|
|/Labs/Users/secrets/DELETE|Geheimen verwijderen.|
|/Labs/Users/secrets/Read|Lezen van geheimen.|
|/Labs/Users/secrets/Write|Toevoegen of wijzigen van geheimen.|
|/Labs/Users/Environments/DELETE|Verwijder omgevingen.|
|/Labs/Users/Environments/Read|Lezen omgevingen.|
|/Labs/Users/Environments/Write|Toevoegen of wijzigen van omgevingen.|
|/Labs/Users/Disks/DELETE|Schijven worden verwijderd.|
|/Labs/Users/Disks/Read|Schijven worden gelezen.|
|/Labs/Users/Disks/Write|Toevoegen of wijzigen van de schijven.|
|/Labs/Users/Disks/Attach/Action|Koppelen en Hallo lease van Hallo schijf toohello virtuele machine maken.|
|/Labs/Users/Disks/detach/Action|Ontkoppel en einde Hallo lease van Hallo schijf toohello virtuele machine gekoppeld.|
|/Labs/customImages/DELETE|Verwijderen van aangepaste installatiekopieën.|
|/Labs/customImages/Read|Lezen van aangepaste installatiekopieën.|
|/Labs/customImages/Write|Toevoegen of wijzigen van aangepaste installatiekopieën.|
|/Labs/serviceRunners/DELETE|Service uitlopers verwijderen.|
|/Labs/serviceRunners/Read|Service uitlopers lezen.|
|/Labs/serviceRunners/Write|Toevoegen of wijzigen van de service uitlopers.|
|/Labs/artifactSources/DELETE|Verwijderen van artefacten gegevensbronnen.|
|/Labs/artifactSources/Read|Artefacten bronnen lezen.|
|/Labs/artifactSources/Write|Toevoegen of wijzigen van artefacten bronnen.|
|/Labs/artifactSources/artifacts/Read|Lezen van artefacten.|
|/Labs/artifactSources/artifacts/GenerateArmTemplate/Action|Genereert een ARM-sjabloon voor Hallo artefact gegeven, uploadt Hallo vereist bestanden tooa storage-account en valideert artefact Hallo gegenereerd.|
|/Labs/artifactSources/armTemplates/Read|Lezen van azure resource manager-sjablonen.|
|/Labs/costs/Read|Kosten worden gelezen.|
|/Labs/costs/Write|Toevoegen of wijzigen van de kosten.|
|/Labs/virtualNetworks/DELETE|Verwijder de virtuele netwerken.|
|/Labs/virtualNetworks/Read|Virtuele netwerken gelezen.|
|/Labs/virtualNetworks/Write|Toevoegen of wijzigen van virtuele netwerken.|
|/Labs/Formulas/DELETE|Verwijder de formules.|
|/Labs/Formulas/Read|Lees de formules.|
|/Labs/Formulas/Write|Toevoegen of wijzigen van formules.|
|/Labs/Schedules/DELETE|Verwijderen van schema's.|
|/Labs/Schedules/Read|Schema's worden gelezen.|
|/Labs/Schedules/Write|Toevoegen of wijzigen van schema's.|
|/Labs/Schedules/Execute/Action|Een schema worden uitgevoerd.|
|/Labs/Schedules/ListApplicable/Action|Geeft een lijst van alle toepasselijke schema 's|
|/Labs/galleryImages/Read|Afbeeldingen worden gelezen.|
|/Labs/policySets/EvaluatePolicies/Action|Lab beleid evalueert.|
|/Labs/policySets/Policies/DELETE|Beleid verwijderen.|
|/Labs/policySets/Policies/Read|Lezen van beleid.|
|/Labs/policySets/Policies/Write|Toevoegen of wijzigen van beleid.|
|/Labs/virtualMachines/DELETE|Verwijder de virtuele machines.|
|/Labs/virtualMachines/Read|Virtuele machines gelezen.|
|/Labs/virtualMachines/Write|Hiermee worden virtuele machines toegevoegd of gewijzigd.|
|/Labs/virtualMachines/start/Action|Een virtuele machine start.|
|/Labs/virtualMachines/Stop/Action|Een virtuele machine stoppen|
|/Labs/virtualMachines/ApplyArtifacts/Action|Artefacten toovirtual machine toepassen.|
|/Labs/virtualMachines/AddDataDisk/Action|Voeg een nieuwe of bestaande gegevens schijf toovirtual machine.|
|/Labs/virtualMachines/DetachDataDisk/Action|Loskoppelen van de opgegeven schijf Hallo van Hallo virtuele machine.|
|/Labs/virtualMachines/claim/Action|Eigenaar worden van een bestaande virtuele machine|
|/Labs/virtualMachines/ListApplicableSchedules/Action|Geeft een lijst van alle toepasselijke schema 's|
|/Labs/virtualMachines/Schedules/DELETE|Verwijderen van schema's.|
|/Labs/virtualMachines/Schedules/Read|Schema's worden gelezen.|
|/Labs/virtualMachines/Schedules/Write|Toevoegen of wijzigen van schema's.|
|/Labs/virtualMachines/Schedules/Execute/Action|Een schema worden uitgevoerd.|
|/Labs/notificationChannels/DELETE|Notificationchannels verwijderen.|
|/Labs/notificationChannels/Read|Notificationchannels lezen.|
|/Labs/notificationChannels/Write|Toevoegen of wijzigen van notificationchannels.|
|/Labs/notificationChannels/Notify/Action|Meldingskanaal tooprovided verzenden.|
|/Schedules/DELETE|Verwijderen van schema's.|
|/Schedules/Read|Schema's worden gelezen.|
|schema's / schrijven|Toevoegen of wijzigen van schema's.|
|/Schedules/Execute/Action|Een schema worden uitgevoerd.|
|/Schedules/Retarget/Action|Updates van een planning doelresource-id.|
|/Locations/Operations/Read|Lees-en schrijfopdrachten.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Bewerking | Beschrijving |
|---|---|
|/databaseAccountNames/Read|Controleert of de naam van beschikbaarheid.|
|/databaseAccounts/Read|Een databaseaccount leest.|
|databaseAccounts/schrijven|Bijwerken van een database-accounts.|
|/databaseAccounts/listKeys/Action|Lijst met sleutels van een databaseaccount|
|/databaseAccounts/regenerateKey/Action|Sleutels van een databaseaccount draaien|
|/databaseAccounts/listConnectionStrings/Action|Hallo-verbindingsreeksen niet ophalen voor een databaseaccount|
|/databaseAccounts/changeResourceGroup/Action|Resourcegroep van een databaseaccount wijzigen|
|/databaseAccounts/failoverPriorityChange/Action|Failover prioriteiten van regio's van een databaseaccount wijzigen. Dit is gebruikte tooperform handmatige failover-bewerking|
|/databaseAccounts/DELETE|Hiermee verwijdert u Hallo database accounts.|
|/databaseAccounts/metricDefinitions/Read|Hallo-databaseaccount leest metrische definities.|
|/databaseAccounts/metrics/Read|Hallo database account metrische gegevens leest.|
|/databaseAccounts/usages/Read|Hallo database account gebruik leest.|
|/databaseAccounts/databases/Collections/metricDefinitions/Read|Hallo verzameling leest metrische definities.|
|/databaseAccounts/databases/Collections/metrics/Read|Hallo verzameling metrische gegevens leest.|
|/databaseAccounts/databases/Collections/usages/Read|Hallo verzameling gebruik leest.|
|/databaseAccounts/databases/metricDefinitions/Read|Hallo database metrische definities lezen|
|/databaseAccounts/databases/metrics/Read|Hallo database metrische gegevens leest.|
|/databaseAccounts/databases/usages/Read|Hallo database gebruik leest.|
|/databaseAccounts/readonlykeys/Read|Hallo-databaseaccount leest readonly sleutels.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Bewerking | Beschrijving |
|---|---|
|/ generateSsoRequest/actie|Genereren van een aanvraag voor het aanmelden bij domein control center.|
|/ validateDomainRegistrationInformation/actie|Aankoop domeinobject valideren zonder deze te verzenden|
|/ checkDomainAvailability/actie|Controleer of een domein aanschaffen is|
|/ listDomainRecommendations/actie|Hallo lijst domein aanbevelingen op basis van trefwoorden ophalen|
|registratie-/ actie|De registerbronprovider Hallo Microsoft Domains voor Hallo-abonnement|
|/ domeinen/lezen|Lijst met domeinen Hallo ophalen|
|/ domeinen/schrijven|Een nieuw domein toevoegen of een bestaande bijgewerkt|
|/ domeinen/verwijderen|Een bestaand domein verwijdert.|
|/Domains/operationresults/Read|De bewerking van een domein ophalen|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Bewerking | Beschrijving |
|---|---|
|/lcsprojects/Read|Microsoft Dynamics Lifecycle Services-projecten die deel uitmaken van de gebruiker tooa weergeven|
|lcsprojects/schrijven|Maken en projecten van Microsoft Dynamics levenscyclus van Services die deel uitmaken van de gebruiker toohello bijwerken. Alleen eigenschappen van Hallo naam en beschrijving kunnen worden bijgewerkt. Hallo-abonnement en de locatie die is gekoppeld aan het Hallo-project kunnen niet worden bijgewerkt nadat het maken|
|/lcsprojects/DELETE|Microsoft Dynamics Lifecycle Services-projecten die deel uitmaken van de gebruiker toohello verwijderen|
|/lcsprojects/clouddeployments/Read|Microsoft Dynamics AX 2012 R3 Evaluation-implementaties in een Microsoft Dynamics Lifecycle Services-project die deel uitmaken van de gebruiker tooa weergeven|
|/lcsprojects/clouddeployments/Write|Microsoft Dynamics AX 2012 R3 evaluatie-implementatie in een project Microsoft Dynamics levenscyclus van Services die deel uitmaken van de gebruiker tooa maken. Implementaties kunnen worden beheerd vanaf de Azure-beheerportal|
|/lcsprojects/connectors/Read|Lezen van connectors die deel uitmaken van tooa Microsoft Dynamics-Services de levenscyclus van project|
|/lcsprojects/connectors/Write|Maken en bijwerken van connectors die deel uitmaken van tooa Microsoft Dynamics-Services de levenscyclus van project|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Bewerking | Beschrijving |
|---|---|
|/ checkNameAvailability/actie|Hiermee wordt de beschikbaarheid van de naamruimte in een bepaald abonnement gecontroleerd.|
|registratie-/ actie|Hallo-abonnement voor Hallo EventHub-resourceprovider geregistreerd en kunnen Hallo maken van EventHub-resources|
|naamruimten/schrijven|Een Namespace-Resource maken en bijwerken van de eigenschappen ervan. Tags en status van Hallo Namespace zijn Hallo-eigenschappen die kunnen worden bijgewerkt.|
|/Namespaces/Read|Hallo-lijst van Namespace resourcebeschrijving ophalen|
|/ naamruimten/verwijderen|Namespace-bron verwijderen|
|/Namespaces/metricDefinitions/Read|Lijst met Namespace metrische Resource beschrijvingen|
|/Namespaces/authorizationRules/Read|Hallo-lijst van de beschrijving van de naamruimten autorisatieregels ophalen.|
|/Namespaces/authorizationRules/Write|Een Namespace niveau autorisatieregels maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/authorizationRules/DELETE|Namespace autorisatieregel verwijderen. Hallo Namespace autorisatie standaardregel kan niet worden verwijderd. |
|/Namespaces/authorizationRules/listkeys/Action|Hallo verbindingsreeks toohello Namespace ophalen|
|/Namespaces/authorizationRules/regenerateKeys/Action|Hallo primaire of secundaire sleutel toohello Resource genereren|
|/Namespaces/eventhubs/Write|Maken of bijwerken EventHub-eigenschappen.|
|/Namespaces/eventhubs/Read|Lijst met beschrijvingen van EventHub-Resource|
|/Namespaces/eventhubs/DELETE|Bewerking toodelete EventHub-Resource|
|/Namespaces/eventHubs/consumergroups/Write|Maken of bijwerken ConsumerGroup eigenschappen.|
|/Namespaces/eventHubs/consumergroups/Read|Lijst met beschrijvingen van de Resource ConsumerGroup ophalen|
|/Namespaces/eventHubs/consumergroups/DELETE|Bewerking toodelete ConsumerGroup Resource|
|/Namespaces/eventhubs/authorizationRules/Read| Hallo-lijst van EventHub-autorisatieregels|
|/Namespaces/eventhubs/authorizationRules/Write|Autorisatieregels EventHub maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/eventhubs/authorizationRules/DELETE|Bewerking toodelete EventHub-autorisatieregels|
|/Namespaces/eventhubs/authorizationRules/listkeys/Action|Hallo verbindingsreeks tooEventHub ophalen|
|/Namespaces/eventhubs/authorizationRules/regenerateKeys/Action|Hallo primaire of secundaire sleutel toohello Resource genereren|
|/Namespaces/diagnosticSettings/Read|Lijst met beschrijvingen van de Resource Namespace diagnostische instellingen|
|/Namespaces/diagnosticSettings/Write|Lijst met beschrijvingen van de Resource Namespace diagnostische instellingen|
|/Namespaces/logDefinitions/Read|Lijst met Namespace logboeken Resource beschrijvingen|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Bewerking | Beschrijving |
|---|---|
|/providers/Features/Read|Hallo-functie van een abonnement ophalen in een opgegeven resourceprovider.|
|/providers/Features/register/Action|Hallo-functie van een abonnement registreren in een opgegeven resourceprovider.|
|/Features/Read|Hallo-functies van een abonnement opgehaald.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Bewerking | Beschrijving |
|---|---|
|clusters/schrijven|Maken of bijwerken van HDInsight-Cluster|
|/clusters/Read|Meer informatie over de HDInsight-Cluster|
|/clusters/DELETE|Een HDInsight-Cluster verwijderen|
|/clusters/changerdpsetting/Action|RDP-instelling voor HDInsight-Cluster wijzigen|
|/clusters/Configurations/Action|Werk de configuratie van de HDInsight-Cluster|
|/clusters/Configurations/Read|HDInsight-Cluster configuraties ophalen|
|/clusters/roles/Resize/Action|Een HDInsight-Cluster vergroten of verkleinen|
|/Locations/Capabilities/Read|Ophalen van abonnement mogelijkheden|
|/Locations/checkNameAvailability/Read|Controleer de naam van de beschikbaarheid|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo abonnement voor de resourceprovider voor importeren/exporteren Hallo registreert en Hiermee kunt u taken voor importeren/exporteren Hallo maken.|
|taken/schrijven|Hiermee maakt u een taak met de opgegeven parameters Hallo of bij te werken Hallo eigenschappen of labels voor de gespecificeerde taak Hallo.|
|/jobs/Read|Hallo-eigenschappen voor de gespecificeerde taak Hallo opgehaald of Hallo lijst met taken geretourneerd.|
|/jobs/listBitLockerKeys/Action|Hallo BitLocker-sleutels voor de gespecificeerde taak Hallo opgehaald.|
|/jobs/DELETE|Hiermee verwijdert u een bestaande taak.|
|/Locations/Read|Hiermee haalt Hallo eigenschappen voor Hallo opgegeven locatie of retourneert Hallo lijst van locaties.|

## <a name="microsoftinsights"></a>Microsoft.Insights

| Bewerking | Beschrijving |
|---|---|
|/ Registreren/actie|Hallo microsoft insights provider registreren|
|/ AlertRules/schrijven|Schrijven tooan waarschuwingsregel configuratie|
|/ AlertRules/verwijderen|Configuratie van een waarschuwingsregel verwijderen|
|AlertRules/leestijd|Configuratie van een waarschuwingsregel lezen|
|/ AlertRules/geactiveerd/actie|Waarschuwingsregel geactiveerd|
|/ AlertRules/opgelost/actie|Waarschuwingsregel opgelost|
|/ AlertRules/beperkt/actie|Waarschuwingsregel is beperkt|
|AlertRules/incidenten/leestijd|Incidentconfiguratie van een waarschuwingsregel lezen|
|MetricDefinitions/leestijd|Metrische definities lezen|
|/EventTypes/Values/Read|Waarden beheergebeurtenistype lezen|
|/EventTypes/digestevents/Read|Samenvatting beheergebeurtenistype lezen|
|Metrische gegevens/leestijd|Metrische gegevens lezen|
|/ LogProfiles/schrijven|Profielconfiguratie voor tooa logboek schrijven|
|/ LogProfiles/verwijderen|Logboek profielen configuratie verwijderen|
|LogProfiles/leestijd|Profielen voor lees-logboek|
|/ AutoscaleSettings/schrijven|Configuratie van instelling voor automatisch schalen tooan schrijven|
|/ AutoscaleSettings/verwijderen|Configuratie-instelling voor automatisch schalen verwijderen|
|AutoscaleSettings/leestijd|Configuratie-instelling voor automatisch schalen lezen|
|/ AutoscaleSettings/Scaleup/actie|Bewerking Omhoog schalen via automatisch schalen|
|/ AutoscaleSettings/Scaledown/actie|Schaal omlaag bewerking automatisch schalen|
|/AutoscaleSettings/providers/Microsoft.Insights/MetricDefinitions/Read|Metrische definities lezen|
|/ ActivityLogAlerts/geactiveerd/actie|Geactiveerde Hallo activiteit logboek waarschuwing|
|/ DiagnosticSettings/schrijven|Configuratie van toodiagnostic schrijven|
|/ DiagnosticSettings/verwijderen|Verwijderen van configuratie van diagnostische instellingen|
|DiagnosticSettings/leestijd|Een configuratie voor de diagnostische instellingen lezen|
|LogDefinitions/leestijd|Logboekdefinities lezen|
|/ ExtendedDiagnosticSettings/schrijven|Configuratie van diagnostische instellingen tooextended schrijven|
|/ ExtendedDiagnosticSettings/verwijderen|Configuratie van diagnostische instellingen voor uitgebreide verwijderd|
|ExtendedDiagnosticSettings/leestijd|Lezen van de configuratie van een uitgebreide diagnostische instellingen|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Registreert een abonnement|
|/checkNameAvailability/Read|Hiermee wordt gecontroleerd of de opgegeven sleutelkluisnaam geldig is en niet wordt gebruikt|
|/vaults/Read|Hallo-eigenschappen van een sleutelkluis weergeven|
|kluizen/schrijven|Maak een nieuwe sleutel kluis of update Hallo eigenschappen van een bestaande sleutelkluis|
|/vaults/DELETE|Een sleutelkluis verwijderen|
|/vaults/Deploy/Action|Hiermee toegang tot toosecrets in een sleutelkluis bij het implementeren van Azure-resources|
|/vaults/secrets/Read|Hallo-eigenschappen van een geheim, maar niet de waarde ervan bekijken|
|/vaults/secrets/Write|Maak een nieuwe geheim of update Hallo waarde van een bestaande geheim|
|/vaults/accessPolicies/Write|Bijwerken van een bestaand toegangsbeleid door samenvoegen of vervangen of Voeg een nieuwe toegang beleid tooa kluis.|
|/deletedVaults/Read|Hallo-eigenschappen van voorlopig verwijderde sleutelkluizen weergeven|
|/Locations/operationResults/Read|Resultaat van controle op Hallo van een bewerking voor de lange termijn|
|/Locations/deletedVaults/Read|Hallo-eigenschappen van een voorlopig verwijderde sleutelkluis weergeven|
|/Locations/deletedVaults/Purge/Action|Een voorlopig verwijderde sleutelkluis opschonen|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Bewerking | Beschrijving |
|---|---|
|/workflows/Read|Hallo werkstroom leest.|
|werkstromen/schrijven|Maken of bijwerken van Hallo-werkstroom.|
|/workflows/DELETE|Hiermee verwijdert u Hallo-werkstroom.|
|/workflows/Run/Action|Start een uitvoering van het Hallo-werkstroom.|
|/workflows/Disable/Action|Hiermee schakelt u Hallo-werkstroom.|
|/workflows/Enable/Action|Hiermee schakelt u Hallo-werkstroom.|
|/workflows/Validate/Action|Hallo werkstroom valideert.|
|/workflows/Move/Action|Werkstroom verplaatst van de bestaande resourcegroep abonnements-id, resourcegroep en/of de naam van tooa andere abonnements-id en/of de naam van.|
|/workflows/listSwagger/Action|Hallo werkstroom swagger definities opgehaald.|
|/workflows/regenerateAccessKey/Action|Hallo toegang sleutel geheimen genereert.|
|/workflows/listCallbackUrl/Action|Hiermee Hallo callback URL voor de werkstroom.|
|/workflows/Versions/Read|Hallo werkstroom versie leest.|
|/workflows/Versions/triggers/listCallbackUrl/Action|Hiermee haalt Hallo callback URL voor de trigger.|
|werkstromen/wordt uitgevoerd/lezen|Hallo werkstroom leest.|
|/workflows/runs/Cancel/Action|Hiermee annuleert u Hallo uitvoeren van een werkstroom.|
|/workflows/runs/Actions/Read|Leest Hallo werkstroom actie uitvoeren.|
|/workflows/runs/Operations/Read|Bewerkingsstatus van de werkstroom Hallo leest.|
|/workflows/triggers/Read|Hallo trigger leest.|
|/workflows/triggers/Run/Action|Hallo trigger worden uitgevoerd.|
|/workflows/triggers/listCallbackUrl/Action|Hiermee haalt Hallo callback URL voor de trigger.|
|/workflows/triggers/histories/Read|Hallo trigger geschiedenisgegevens worden gelezen.|
|/workflows/triggers/histories/resubmit/Action|Opnieuw indient Hallo werkstroom activeren.|
|/workflows/accessKeys/Read|Hallo-toegangssleutel leest.|
|/workflows/accessKeys/Write|Maken of bijwerken van Hallo toegangssleutel.|
|/workflows/accessKeys/DELETE|Hiermee verwijdert u Hallo toegangssleutel.|
|/workflows/accessKeys/List/Action|Geeft een lijst Hallo toegang sleutel geheimen.|
|/workflows/accessKeys/Regenerate/Action|Hallo toegang sleutel geheimen genereert.|
|/Locations/workflows/Validate/Action|Hallo werkstroom valideert.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo-abonnement voor Hallo machine learning web service-resourceprovider geregistreerd en kunnen Hallo maken van webservices.|
|webServices/actie|Regionale Web Service-eigenschappen voor ondersteunde regio's maken|
|/commitmentPlans/Read|Een Machine streven trainingsplan lezen|
|commitmentPlans/schrijven|Maken of bijwerken van een Machine Learning streven plannen|
|/commitmentPlans/DELETE|Een Machine streven trainingsplan verwijderen|
|/commitmentPlans/join/Action|Lid worden van een Machine streven trainingsplan|
|/commitmentPlans/commitmentAssociations/Read|Lezen van een Machine Learning-streven Plan koppeling|
|/commitmentPlans/commitmentAssociations/Move/Action|Verplaatsen van een Machine Learning-streven Plan koppeling|
|Werkruimten/leestijd|Lezen van een Machine Learning-werkruimte|
|/ Werkruimten/schrijven|Een Machine Learning-werkruimte gemaakt of bijgewerkt|
|-Werkruimten, verwijderen|Verwijderen van een Machine Learning-werkruimte|
|/ Werkruimten/listworkspacekeys/actie|Lijst met sleutels voor een Machine Learning-werkruimte|
|/ Werkruimten/resyncstoragekeys/actie|Sleutels van opslagaccount geconfigureerd voor een Machine Learning-werkruimte synchroniseren|
|/webServices/Read|Lezen van een Machine Learning-webservice|
|webServices/schrijven|Maken of bijwerken van een Machine Learning-webservice|
|/webServices/DELETE|Verwijderen van een Machine Learning-webservice|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Bewerking | Beschrijving |
|---|---|
|/agreements/Offers/plans/Read|Retourneren van een overeenkomst voor een bepaalde marketplace-item|
|/agreements/Offers/plans/Sign/Action|Meld u aan een overeenkomst voor een bepaalde marketplace-item|
|/agreements/Offers/plans/Cancel/Action|Annuleren van een overeenkomst voor een bepaalde marketplace-item|

## <a name="microsoftmedia"></a>Microsoft.Media

| Bewerking | Beschrijving |
|---|---|
|/mediaservices/Read||
|mediaservices/schrijven||
|/mediaservices/DELETE||
|/mediaservices/regenerateKey/Action||
|/mediaservices/listKeys/Action||
|/mediaservices/syncStorageKeys/Action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Registreert de Hallo-abonnement|
|/ unregister/actie|Heft de registratie van Hallo-abonnement|
|/ checkTrafficManagerNameAvailability/actie|Controleert de beschikbaarheid Hallo van een Traffic Manager ten opzichte van DNS-naam.|
|/dnszones/Read|Hallo DNS-zone, in JSON-indeling, ophalen. Hallo zone-eigenschappen bevatten labels, etag, numberOfRecordSets en maxNumberOfRecordSets. Houd er rekening mee dat deze opdracht niet Hallo recordsets in de zone Hallo ophaalt.|
|dnszones/schrijven|Maken of bijwerken van een DNS-zone binnen een resourcegroep.  Gebruikte tooupdate Hallo labels van een DNS-zone-resource. Houd er rekening mee deze opdracht kan niet worden gebruikt toocreate of update recordsets binnen Hallo zone.|
|/dnszones/DELETE|Verwijder Hallo DNS-zone, in JSON-indeling. Hallo zone-eigenschappen bevatten labels, etag, numberOfRecordSets en maxNumberOfRecordSets.|
|/dnszones/MX/Read|Hallo-recordset van het type 'MX', in JSON-indeling ophalen. Hallo-Recordset omvat een lijst met records, alsmede Hallo TTL, labels en etag.|
|/dnszones/MX/Write|Maken of bijwerken van een recordset van het type 'MX' binnen een DNS-zone. Hallo records opgegeven wordt vervangen door de huidige records in de recordset Hallo Hallo.|
|/dnszones/MX/DELETE|Verwijder Hallo-recordset met een bepaalde naam en typ 'MX' uit een DNS-zone.|
|/dnszones/NS/Read|DNS-recordset van het type NS opgehaald|
|/dnszones/NS/Write|Maken of bijwerken van DNS-recordset van het type NS|
|/dnszones/NS/DELETE|Hiermee verwijdert u Hallo DNS-recordset van het type NS|
|/dnszones/AAAA/Read|Hallo-recordset van het type 'AAAA', in JSON-indeling ophalen. Hallo-Recordset omvat een lijst met records, alsmede Hallo TTL, labels en etag.|
|/dnszones/AAAA/Write|Maken of bijwerken van een recordset van het type 'AAAA' binnen een DNS-zone. Hallo records opgegeven wordt vervangen door de huidige records in de recordset Hallo Hallo.|
|/dnszones/AAAA/DELETE|Verwijder Hallo-recordset met een bepaalde naam en typ 'AAAA' uit een DNS-zone.|
|/dnszones/CNAME/Read|Hallo-recordset van het type 'CNAME', in JSON-indeling ophalen. Hallo-Recordset bevat Hallo TTL, labels en etag.|
|/dnszones/CNAME/Write|Maken of bijwerken van een recordset van het type 'CNAME' binnen een DNS-zone. Hallo records opgegeven wordt vervangen door de huidige records in de recordset Hallo Hallo.|
|/dnszones/CNAME/DELETE|Verwijder Hallo-recordset met een bepaalde naam en typ 'CNAME' uit een DNS-zone.|
|/dnszones/SOA/Read|DNS-recordset van het type SOA opgehaald|
|/dnszones/SOA/Write|Maken of bijwerken van DNS-recordset van het type SOA|
|/dnszones/SRV/Read|Hallo-recordset van het type 'SRV', in JSON-indeling ophalen. Hallo-Recordset omvat een lijst met records, alsmede Hallo TTL, labels en etag.|
|/dnszones/SRV/Write|Maken of bijwerken van de recordset van het type SRV|
|/dnszones/SRV/DELETE|Verwijder Hallo-recordset met een bepaalde naam en typ 'SRV' uit een DNS-zone.|
|/dnszones/PTR/Read|Hallo-recordset van het type 'PTR, in JSON-indeling ophalen. Hallo-Recordset omvat een lijst met records, alsmede Hallo TTL, labels en etag.|
|/dnszones/PTR/Write|Maken of bijwerken van een recordset van het type 'PTR' binnen een DNS-zone. Hallo records opgegeven wordt vervangen door de huidige records in de recordset Hallo Hallo.|
|/dnszones/PTR/DELETE|Verwijder Hallo-recordset met een bepaalde naam en typ 'PTR' uit een DNS-zone.|
|/dnszones/A/Read|Recordset van het type "A" hello ophalen in JSON-indeling. Hallo-Recordset omvat een lijst met records, alsmede Hallo TTL, labels en etag.|
|/dnszones/A/Write|Maken of bijwerken van een recordset van het type "A" binnen een DNS-zone. Hallo records opgegeven wordt vervangen door de huidige records in de recordset Hallo Hallo.|
|/dnszones/A/DELETE|Verwijder Hallo-recordset met een bepaalde naam en typt u "A" uit een DNS-zone.|
|/dnszones/txt/Read|Hallo-recordset van het type 'TXT', in JSON-indeling ophalen. Hallo-Recordset omvat een lijst met records, alsmede Hallo TTL, labels en etag.|
|/dnszones/txt/Write|Maken of bijwerken van een recordset van het type 'TXT' binnen een DNS-zone. Hallo records opgegeven wordt vervangen door de huidige records in de recordset Hallo Hallo.|
|/dnszones/txt/DELETE|Verwijder Hallo-recordset met een bepaalde naam en typ 'TXT' uit een DNS-zone.|
|/dnszones/recordsets/Read|DNS-recordsets in verschillende typen opgehaald|
|/networkInterfaces/Read|Haalt de definitie van een netwerkinterface. |
|networkInterfaces/schrijven|Een netwerkinterface maken of bijwerken van een bestaande netwerkinterface. |
|/networkInterfaces/join/Action|Lid wordt van een virtuele Machine tooa-netwerkinterface|
|/networkInterfaces/DELETE|Hiermee verwijdert u een netwerkinterface|
|/networkInterfaces/effectiveRouteTable/Action|De routetabel is geconfigureerd op de netwerkinterface van Hallo Vm ophalen|
|/networkInterfaces/effectiveNetworkSecurityGroups/Action|Netwerkbeveiligingsgroepen geconfigureerde op Network Interface van Hallo Vm ophalen|
|/networkInterfaces/loadBalancers/Read|Haalt alle Hallo load balancers die Hallo netwerkinterface deel uitmaakt van|
|/networkInterfaces/ipconfigurations/Read|Hiermee haalt u de definitie van de IP-configuratie voor een netwerk-interface. |
|/publicIPAddresses/Read|De definitie van een openbaar IP-adres ophalen.|
|publicIPAddresses/schrijven|Een openbaar IP-adres maken of bijwerken van een bestaand openbaar IP-adres. |
|/publicIPAddresses/DELETE|Hiermee verwijdert u een openbaar IP-adres.|
|/publicIPAddresses/join/Action|Koppelt een openbare IP-adres|
|/routeFilters/Read|De definitie van een route filter ophalen|
|/routeFilters/join/Action|Lid wordt van een routefilter|
|/routeFilters/DELETE|Hiermee verwijdert u een route filterdefinitie|
|routeFilters/schrijven|Een routefilter maken of bijwerken van een bestaand rotue-filter|
|/routeFilters/Rules/Read|De definitie van een route filter regel ophalen|
|/routeFilters/Rules/Write|Een filterregel route maken of bijwerken van een bestaande route filterregel|
|/routeFilters/Rules/DELETE|Hiermee verwijdert u een route regel filterdefinitie|
|/networkWatchers/Read|Hallo-watcher netwerkdefinitie ophalen|
|networkWatchers/schrijven|Een netwerk-watcher maken of bijwerken van een bestaande netwerk-watcher|
|/networkWatchers/DELETE|Hiermee verwijdert u een netwerk-watcher|
|/networkWatchers/configureFlowLog/Action|Hiermee configureert u stroom logboekregistratie voor een doelbron.|
|/networkWatchers/ipFlowVerify/Action|Retourneert of hello-pakket wordt toegestaan of geweigerd tooor van een specifieke bestemming.|
|/networkWatchers/nextHop/Action|Volgend hoptype Hallo retourneren en vervolgens hopen dat IP-adres voor een opgegeven doel- en IP-doeladres.|
|/networkWatchers/queryFlowLogStatus/Action|Haalt status Hallo van logboekregistratie voor een bron-stroom.|
|/networkWatchers/queryTroubleshootResult/Action|Hallo probleemoplossing resultaat Hallo eerder is uitgevoerd of wordt momenteel uitgevoerd probleemoplossing bewerking opgehaald.|
|/networkWatchers/securityGroupView/Action|Hallo geconfigureerd en effectieve netwerkbeveiligingsgroepen toegepast op een virtuele machine weergeven.|
|/networkWatchers/Topology/Action|Hiermee haalt de weergave van resources en hun relaties in een netwerk-niveau in een resourcegroep.|
|/networkWatchers/Troubleshoot/Action|Start het oplossen van een resource netwerken in Azure.|
|/networkWatchers/packetCaptures/queryStatus/Action|Hiermee haalt u informatie over eigenschappen en de status van een pakket vastleggen resource.|
|/networkWatchers/packetCaptures/Stop/Action|Hallo opnamesessie pakket uitgevoerd stoppen.|
|/networkWatchers/packetCaptures/Read|Hallo pakket vastleggen definitie ophalen|
|/networkWatchers/packetCaptures/Write|Maakt een pakketopname|
|/networkWatchers/packetCaptures/DELETE|Hiermee verwijdert u een pakketopname|
|/loadBalancers/Read|De definitie van een load balancer ophalen|
|loadBalancers/schrijven|Een load balancer maken of bijwerken van een bestaande load balancer|
|/loadBalancers/DELETE|Hiermee verwijdert u een load balancer|
|/loadBalancers/networkInterfaces/Read|Verwijzingen ophalen tooall Hallo netwerkinterfaces onder een load balancer|
|/loadBalancers/loadBalancingRules/Read|Een load balancer load taakverdeling ophalen|
|/loadBalancers/backendAddressPools/Read|Een definitie van het groep back-end-adres van load balancer ophalen|
|/loadBalancers/backendAddressPools/join/Action|Lid wordt van een back-endadresgroep voor load balancer|
|/loadBalancers/inboundNatPools/Read|Een load balancer ophalen inkomende nat-pooldefinitie|
|/loadBalancers/inboundNatPools/join/Action|Lid wordt van een load balancer binnenkomende nat-pool|
|/loadBalancers/inboundNatRules/Read|Een load balancer ophalen inkomende nat-regel definiëren|
|/loadBalancers/inboundNatRules/Write|Een binnenkomende nat-regel van load balancer maken of bijwerken van een bestaande load balancer binnenkomende nat-regel|
|/loadBalancers/inboundNatRules/DELETE|Een binnenkomende nat-regel van load balancer verwijderen|
|/loadBalancers/inboundNatRules/join/Action|Lid wordt van een load balancer binnenkomende nat-regel|
|/loadBalancers/outboundNatRules/Read|Een definitie voor uitgaande nat-regel van load balancer opgehaald|
|/loadBalancers/probes/Read|Een load balancer-test opgehaald|
|/loadBalancers/virtualMachines/Read|Verwijzingen ophalen tooall Hallo virtuele machines onder een load balancer|
|/loadBalancers/frontendIPConfigurations/Read|Een definitie van load balancer frontend IP-configuratie ophalen|
|/trafficManagerGeographicHierarchies/Read|Hallo Traffic Manager geografisch hiërarchie opgehaald die regio's die kunnen worden gebruikt met Hallo geografische verkeersrouteringsmethode bevat|
|/bgpServiceCommunities/Read|Bgp-Service-community's ophalen|
|/applicationGatewayAvailableWafRuleSets/Read|Toepassingsgateway beschikbaar Waf regelsets opgehaald|
|/virtualNetworks/Read|Definitie van Hallo virtueel netwerk ophalen|
|virtualNetworks/schrijven|Een virtueel netwerk maken of bijwerken van een bestaand virtueel netwerk|
|/virtualNetworks/DELETE|Hiermee verwijdert u een virtueel netwerk|
|/virtualNetworks/peer/Action|Een virtueel netwerk met een ander virtueel netwerk samenwerkt|
|/virtualNetworks/virtualNetworkPeerings/Read|De definitie van een virtueel netwerk peering ophalen|
|/virtualNetworks/virtualNetworkPeerings/Write|Een virtueel netwerk peering of een bestaande virtuele netwerk-peering bijwerken|
|/virtualNetworks/virtualNetworkPeerings/DELETE|Hiermee verwijdert u een virtueel netwerk peering|
|/virtualNetworks/subnets/Read|De subnet-definitie van een virtueel netwerk ophalen|
|/virtualNetworks/subnets/Write|Een virtueel netwerksubnet maken of bijwerken van een bestaand virtueel netwerksubnet|
|/virtualNetworks/subnets/DELETE|Hiermee verwijdert u een virtueel netwerksubnet|
|/virtualNetworks/subnets/join/Action|Lid wordt van een virtueel netwerk|
|/virtualNetworks/subnets/joinViaServiceTunnel/Action|Koppelt de resource, zoals tooa Service Tunneling ingeschakeld subnet opslagaccount of de SQL-database.|
|/virtualNetworks/subnets/virtualMachines/Read|Verwijzingen ophalen tooall Hallo virtuele machines in een virtueel netwerksubnet|
|/virtualNetworks/checkIpAddressAvailability/Read|Controleer of IP-adres beschikbaar op Hallo van de opgegeven virtuele netwerk is|
|/virtualNetworks/virtualMachines/Read|Verwijzingen ophalen tooall Hallo virtuele machines in een virtueel netwerk|
|/expressRouteServiceProviders/Read|Express Route-serviceproviders opgehaald|
|/dnsoperationresults/Read|Resultaten van een DNS-bewerking opgehaald|
|/localnetworkgateways/Read|LocalNetworkGateway opgehaald|
|localnetworkgateways/schrijven|Maken of bijwerken van een bestaande LocalNetworkGateway|
|/localnetworkgateways/DELETE|Hiermee verwijdert u LocalNetworkGateway|
|/trafficManagerProfiles/Read|Hallo Traffic Manager-profielconfiguratie ophalen. Dit omvat DNS-instellingen, instellingen voor verkeersroutering, instellingen voor eindpuntcontrole en Hallo lijst met eindpunten die worden gerouteerd door dit Traffic Manager-profiel.|
|trafficManagerProfiles/schrijven|Een Traffic Manager-profiel maken of wijzigen van Hallo configuratie van een bestaand Traffic Manager-profiel. Dit omvat inschakelen of uitschakelen van een profiel en DNS-instellingen, instellingen voor verkeersroutering of instellingen voor eindpuntcontrole wijzigen. Eindpunten die worden gerouteerd door Hallo Traffic Manager-profiel kunnen worden toegevoegd, verwijderd, ingeschakeld of uitgeschakeld.|
|/trafficManagerProfiles/DELETE|Hallo Traffic Manager-profiel verwijderen. Alle instellingen die zijn gekoppeld aan Hallo Traffic Manager-profiel niet verloren en het Hallo-profiel kan niet meer worden gebruikt tooroute verkeer.|
|/dnsoperationstatuses/Read|Hiermee wordt de status van een DNS-bewerking opgehaald |
|/Operations/Read|Beschikbare bewerkingen ophalen|
|/expressRouteCircuits/Read|Een ExpressRouteCircuit ophalen|
|expressRouteCircuits/schrijven|Maken of bijwerken van een bestaande ExpressRouteCircuit|
|/expressRouteCircuits/DELETE|Een ExpressRouteCircuit verwijderen|
|/expressRouteCircuits/stats/Read|Een ExpressRouteCircuit Stat opgehaald|
|/expressRouteCircuits/peerings/Read|Een ExpressRouteCircuit Peering opgehaald|
|/expressRouteCircuits/peerings/Write|Maken of bijwerken van een bestaande Peering ExpressRouteCircuit|
|/expressRouteCircuits/peerings/DELETE|Hiermee verwijdert u een ExpressRouteCircuit Peering|
|/expressRouteCircuits/peerings/arpTables/Action|Een ExpressRouteCircuit Peering ArpTable opgehaald|
|/expressRouteCircuits/peerings/routeTables/Action|Een ExpressRouteCircuit Peering migratiestatus opgehaald|
|/expressRouteCircuits/peerings /<br>routeTablesSummary/actie|Een overzicht van ExpressRouteCircuit Peering migratiestatus opgehaald|
|/expressRouteCircuits/peerings/stats/Read|Een ExpressRouteCircuit Peering statistieken opgehaald|
|/expressRouteCircuits/authorizations/Read|Een vergunning ExpressRouteCircuit opgehaald|
|/expressRouteCircuits/authorizations/Write|Maken of bijwerken van een bestaande ExpressRouteCircuit-autorisatie|
|/expressRouteCircuits/authorizations/DELETE|Hiermee verwijdert u een ExpressRouteCircuit-autorisatie|
|/Connections/Read|VirtualNetworkGatewayConnection opgehaald|
|verbindingen/schrijven|Maken of bijwerken van een bestaande VirtualNetworkGatewayConnection|
|/Connections/DELETE|Hiermee verwijdert u VirtualNetworkGatewayConnection|
|/Connections/sharedKey/Read|VirtualNetworkGatewayConnection SharedKey opgehaald|
|/Connections/sharedKey/Write|Maken of bijwerken van een bestaande VirtualNetworkGatewayConnection SharedKey|
|/networkSecurityGroups/Read|Een definitie van een netwerk opgehaald|
|networkSecurityGroups/schrijven|Een netwerkbeveiligingsgroep maken of bijwerken van een bestaande netwerkbeveiligingsgroep|
|/networkSecurityGroups/DELETE|Hiermee wordt een netwerkbeveiligingsgroep verwijderd|
|/networkSecurityGroups/join/Action|Lid wordt van een netwerkbeveiligingsgroep|
|/networkSecurityGroups/defaultSecurityRules/Read|Een standaardbeveiligingsregeldefinitie ophalen opgehaald|
|/networkSecurityGroups/securityRules/Read|Een beveiligingsregeldefinitie ophalen opgehaald|
|/networkSecurityGroups/securityRules/Write|Een beveiligingsregel maken of een bestaande beveiligingsregel bijwerken|
|/networkSecurityGroups/securityRules/DELETE|Hiermee verwijdert u een beveiligingsregel|
|/applicationGateways/Read|Een application gateway opgehaald|
|applicationGateways/schrijven|Een toepassingsgateway maken of bijwerken van een application gateway|
|/applicationGateways/DELETE|Een toepassingsgateway verwijderen|
|/applicationGateways/backendhealth/Action|Een back-end toepassingsstatus van de gateway opgehaald|
|/applicationGateways/start/Action|Een application gateway wordt gestart|
|/applicationGateways/Stop/Action|Een application gateway wordt gestopt|
|/applicationGateways/backendAddressPools/join/Action|Een application gateway back-end-adresgroep toevoegen|
|/routeTables/Read|Een routetabeldefinitie opgehaald|
|routeTables/schrijven|Een routetabel maken of een bestaande routetabel bijwerken|
|/routeTables/DELETE|Een routetabeldefinitie verwijderen|
|/routeTables/join/Action|Een routetabel joins|
|/routeTables/routes/Read|De definitie van een route ophalen|
|/routeTables/routes/Write|Een route maken of een bestaande route bijwerken|
|/routeTables/routes/DELETE|Hiermee verwijdert u de definitie van een route|
|/Locations/operationResults/Read|Het bewerkingsresultaat van een asynchrone post- of DELETE-bewerking opgehaald|
|/Locations/checkDnsNameAvailability/Read|Controleert of de DNS-label is beschikbaar op Hallo opgegeven locatie|
|/Locations/usages/Read|Hallo resources meetgegevens voor softwaregebruik opgehaald|
|/Locations/Operations/Read|Bewerkingsresource ophalen die de status van een asynchrone bewerking vertegenwoordigt|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo-abonnement voor Hallo NotifciationHubs resourceprovider registreert en wordt Hallo maken van naamruimten en NotificationHubs|
|/ CheckNamespaceAvailability/actie|Controleert of de naam van een bepaalde Namespace-bron beschikbaar in Hallo NotificationHub service is.|
|Naamruimten/schrijftijd|Een Namespace-Resource maken en bijwerken van de eigenschappen ervan. Tags en status van Hallo Namespace zijn Hallo-eigenschappen die kunnen worden bijgewerkt.|
|Naamruimten/leestijd|Hallo-lijst van Namespace resourcebeschrijving ophalen|
|Naamruimten, verwijderen|Namespace-bron verwijderen|
|/ Naamruimten/authorizationRules/actie|Hallo-lijst van de beschrijving van de naamruimten autorisatieregels ophalen.|
|/ Naamruimten/CheckNotificationHubAvailability/actie|Hiermee wordt gecontroleerd of de NotificationHub-naam beschikbaar is binnen een naamruimte.|
|Naamruimten/authorizationRules/schrijftijd|Een Namespace niveau autorisatieregels maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|Naamruimten/authorizationRules/leestijd|Hallo-lijst van de beschrijving van de naamruimten autorisatieregels ophalen.|
|Naamruimten, authorizationRules/verwijderen|Namespace autorisatieregel verwijderen. Hallo Namespace autorisatie standaardregel kan niet worden verwijderd. |
|/ Naamruimten/authorizationRules/listkeys/actie|Hallo verbindingsreeks toohello Namespace ophalen|
|/ Naamruimten/authorizationRules/regenerateKeys/actie|Namespace autorisatie regel opnieuw genereren van primaire/secundaire sleutel, geef Hallo sleutel die toobe behoeften opnieuw gegenereerd|
|Naamruimten/NotificationHubs/schrijftijd|Een Notification Hub maken en bijwerken van de eigenschappen ervan. De eigenschappen zijn hoofdzakelijk PNS-referenties. Autorisatieregels en TTL|
|Naamruimten/NotificationHubs/leestijd|De lijst met beschrijvingen van resources voor Notification Hub ophalen|
|Naamruimten, NotificationHubs/verwijderen|Notification Hub-bron verwijderen|
|/ Naamruimten/NotificationHubs/authorizationRules/actie|Hallo-lijst van de Notification Hub-autorisatieregels|
|/ Naamruimten/NotificationHubs/pnsCredentials/actie|Alle Notification Hub PNS referenties ophalen. Dit omvat, WNS, MPNS, APNS, GCM en Baidu-referenties|
|/ Naamruimten/NotificationHubs/debugSend/actie|Een testpushmelding verzenden.|
|Naamruimten/NotificationHubs/metricDefinitions/leestijd|Lijst met Namespace metrische Resource beschrijvingen|
|/Namespaces/NotificationHubs /<br>authorizationRules/schrijven|Notification Hub-autorisatieregels maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/NotificationHubs /<br>authorizationRules leestijd|Hallo-lijst van de Notification Hub-autorisatieregels|
|/Namespaces/NotificationHubs /<br>authorizationRules/verwijderen|Verificatieregels voor Notification Hub verwijderen|
|/Namespaces/NotificationHubs /<br>listkeys-authorizationRules/actie|Hallo verbindingsreeks toohello Notification Hub ophalen|
|/Namespaces/NotificationHubs /<br>regenerateKeys-authorizationRules/actie|Notification Hub autorisatie regel opnieuw genereren van primaire/secundaire sleutel, geef Hallo sleutel die toobe behoeften opnieuw gegenereerd|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Een abonnement tooa-resourceprovider registreren.|
|/linkTargets/Read|Een lijst met bestaande accounts die niet gekoppeld aan een Azure-abonnement zijn. toolink deze Azure-abonnement tooa werkruimte, gebruiken een klant-id geretourneerd door deze bewerking in Hallo klant-id-eigenschap van Hallo bewerking werkruimte maken.|
|werkruimten/schrijven|Maakt een nieuwe werkruimte of koppelingen tooan bestaande werkruimte doordat Hallo klant-id van de bestaande werkruimte Hallo.|
|/Workspaces/Read|Een bestaande werkruimte opgehaald|
|/Workspaces/DELETE|Hiermee verwijdert u een werkruimte. Als de Hallo werkruimte is gekoppeld Hallo tooan bestaande werkruimte vervolgens tijdens het maken werkruimte was gekoppelde toois niet verwijderd.|
|/Workspaces/generateregistrationcertificate/Action|Genereert Registratiecertificaat voor Hallo-werkruimte. Dit certificaat is gebruikte tooconnect Microsoft System Center Operation Manager toohello werkruimte.|
|/Workspaces/sharedKeys/Action|Hallo gedeelde sleutels voor Hallo werkruimte opgehaald. Deze sleutels zijn werkruimte toohello gebruikte tooconnect Microsoft Operational Insights-agents.|
|/Workspaces/Search/Action|Een zoekopdracht wordt uitgevoerd|
|/Workspaces/Datasources/Read|Gegevensbronnen ophalen onder een werkruimte.|
|/Workspaces/Datasources/Write|Gegevensbronnen onder een werkruimte maken of bijwerken.|
|/Workspaces/Datasources/DELETE|Verwijder de gegevensbronnen onder een werkruimte.|
|/Workspaces/managementGroups/Read|Hiermee haalt Hallo namen en metagegevens voor System Center Operations Manager management groepen verbonden toothis werkruimte.|
|/Workspaces/schema/Read|Hiermee haalt u Hallo search schema voor Hallo-werkruimte.  Search schema bevat Hallo blootgesteld velden en hun typen.|
|/Workspaces/usages/Read|Hiermee haalt gebruiksgegevens voor een werkruimte inclusief Hallo en de hoeveelheid gegevens gelezen door Hallo-werkruimte.|
|/Workspaces/intelligencepacks/Read|Geeft een lijst van alle intelligence packs die zichtbaar zijn voor een bepaalde worksapce en ook wordt aangegeven of pack Hallo is ingeschakeld of uitgeschakeld voor die werkruimte.|
|/Workspaces/intelligencepacks/Enable/Action|Hiermee kunt een intelligence pack voor een bepaalde werkruimte.|
|/Workspaces/intelligencepacks/Disable/Action|Hiermee schakelt u een intelligence pack voor een bepaalde werkruimte.|
|/Workspaces/sharedKeys/Read|Hallo gedeelde sleutels voor Hallo werkruimte opgehaald. Deze sleutels zijn werkruimte toohello gebruikte tooconnect Microsoft Operational Insights-agents.|
|/Workspaces/savedSearches/Read|Een opgeslagen zoekopdracht opgehaald|
|/Workspaces/savedSearches/Write|Hiermee maakt u een opgeslagen zoekopdracht|
|/Workspaces/savedSearches/DELETE|Hiermee verwijdert u een opgeslagen zoekopdracht|
|/Workspaces/storageinsightconfigs/Write|Maakt een nieuwe opslagconfiguratie. Deze configuraties zijn gebruikte toopull gegevens vanaf een locatie in een bestaand opslagaccount.|
|/Workspaces/storageinsightconfigs/Read|Hiermee haalt u een configuratie van de opslag.|
|/Workspaces/storageinsightconfigs/DELETE|Hiermee verwijdert u een configuratie van de opslag. Hiermee stopt u Microsoft Operational Insights van lezen van gegevens van Hallo storage-account.|
|/Workspaces/configurationScopes/Read|Configuratiebereik ophalen|
|/Workspaces/configurationScopes/Write|Configuratiebereik instellen|
|/Workspaces/configurationScopes/DELETE|Configuratiebereik verwijderen|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Een abonnement tooa-resourceprovider registreren.|
|oplossingen/schrijven|Nieuwe OMS-oplossing maken|
|/Solutions/Read|Ophalen van OMS oplossing afgesloten|
|/Solutions/DELETE|Verwijderen van bestaande OMS-oplossing|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Bewerking | Beschrijving |
|---|---|
|/ Kluizen/backupJobsExport/actie|Exporttaken|
|Kluizen/schrijftijd|Met de bewerking Kluis maken wordt een Azure-resource van het type vault gemaakt.|
|Kluizen/leestijd|Hallo kluis ophalen-bewerking een object dat Azure-resource van het type 'kluis' hello opgehaald|
|/ Kluizen/verwijderen|Hallo kluis verwijderen bewerking verwijderingen Hallo opgegeven Azure-resource van het type 'kluis'|
|Kluizen/refreshContainers/leestijd|Lijst met Hallo-container te vernieuwen|
|Kluizen/backupJobsExport/operationResults/leestijd|Retourneert hello resultaat van taak bewerking Export.|
|Kluizen/backupOperationResults/leestijd|Hiermee wordt het resultaat van de back-upbewerking voor een Recovery Services-kluis geretourneerd.|
|Kluizen/monitoringAlerts/leestijd|Hiermee haalt Hallo waarschuwingen voor Hallo Recovery services-kluis.|
|/Vaults/monitoringAlerts / {uniqueAlertId} / lezen|Details van waarschuwing Hallo Hallo opgehaald.|
|Kluizen/backupSecurityPIN/leestijd|Beveiliging PINCODE retourneert informatie voor Recovery Services-kluis.|
|/vaults/replicationEvents/Read|Alle gebeurtenissen lezen|
|Kluizen/backupProtectableItems/leestijd|Hiermee wordt een lijst met alle beveiligbare items opgehaald.|
|/vaults/replicationFabrics/Read|Alle Fabrics lezen|
|/vaults/replicationFabrics/Write|Maken of bijwerken van een Fabrics|
|/vaults/replicationFabrics/Remove/Action|Infrastructuur verwijderen|
|/vaults/replicationFabrics/checkConsistency/Action|Consistentie van de controles van Hallo Fabric|
|/vaults/replicationFabrics/DELETE|Verwijderen van eventuele Fabrics|
|/vaults/replicationFabrics/renewcertificate/Action||
|/vaults/replicationFabrics/deployProcessServerImage/Action|Proces serverinstallatiekopie te implementeren|
|/vaults/replicationFabrics/reassociateGateway/Action|Gateway opnieuw koppelen|
|kluizen/replicationFabrics/replicationRecoveryServicesProviders /<br>Lezen|Een Recovery Services-Providers lezen|
|kluizen/replicationFabrics/replicationRecoveryServicesProviders /<br>verwijderen/actie|Recovery Services-Provider verwijderen|
|kluizen/replicationFabrics/replicationRecoveryServicesProviders /<br>verwijderen|Verwijderen van een Recovery Services-Providers|
|kluizen/replicationFabrics/replicationRecoveryServicesProviders /<br>refreshProvider/actie|Vernieuw de Provider|
|/vaults/replicationFabrics/replicationStorageClassifications/Read|Alle Opslagclassificaties lezen|
|kluizen/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings leestijd|Alle toewijzingen van de classificatie opslag lezen|
|kluizen/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/schrijven|Maken of bijwerken van alle toewijzingen van de classificatie opslag|
|kluizen/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/verwijderen|Alle toewijzingen van de classificatie opslag verwijderen|
|/vaults/replicationFabrics/replicationvCenters/Read|Lezen van taken|
|/vaults/replicationFabrics/replicationvCenters/Write|Alle taken maken of bijwerken|
|/vaults/replicationFabrics/replicationvCenters/DELETE|Taken verwijderen|
|/vaults/replicationFabrics/replicationNetworks/Read|Geen netwerken lezen|
|kluizen/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings leestijd|Alle Netwerktoewijzingen lezen|
|kluizen/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/schrijven|Maken of bijwerken van eventuele Netwerktoewijzingen|
|kluizen/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/verwijderen|Eventuele Netwerktoewijzingen verwijderen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>Lezen|Beveiliging-Containers gelezen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>discoverProtectableItem/actie|Beveiligbare Item detecteren|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>schrijven|Maken of bijwerken van alle Containers beveiliging|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>verwijderen/actie|De Beveiligingscontainer verwijderen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>switchprotection/actie|Switch Protection Container|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectableItems leestijd|Alle beveiligbare objecten lezen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings leestijd|Alle toewijzingen van de Container beveiliging lezen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/schrijven|Maken of bijwerken van alle toewijzingen van de Container beveiliging|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/verwijderen/actie|Beveiliging Container toewijzing verwijderen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/verwijderen|Alle toewijzingen van de Container beveiliging verwijderen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems leestijd|Alle beveiligde Items lezen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/schrijven|Maken of bijwerken van alle beveiligde Items|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/verwijderen|Verwijder alle beveiligde Items|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/verwijderen/actie|Het beveiligde Item verwijderen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>plannedFailover-replicationProtectedItems/actie|Geplande Failover|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>unplannedFailover-replicationProtectedItems/actie|Failover|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>testFailover-replicationProtectedItems/actie|Failover testen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>testFailoverCleanup-replicationProtectedItems/actie|Het opruimen van testfailover|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>failoverCommit-replicationProtectedItems/actie|Failover doorvoeren|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems, beveiligt/actie|Beveiligde Item opnieuw beveiligen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>updateMobilityService-replicationProtectedItems/actie|Bijwerken van de Mobility-Service|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>repairReplication-replicationProtectedItems/actie|Reparatie replicatie|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>applyRecoveryPoint-replicationProtectedItems/actie|Herstelpunt toepassen|
|kluizen/replicationFabrics/replicationProtectionContainers /<br>recoveryPoints replicationProtectedItems leestijd|Replicatie herstelpunten lezen|
|/vaults/replicationPolicies/Read|Lezen van beleid|
|/vaults/replicationPolicies/Write|Beleid maken of bijwerken|
|/vaults/replicationPolicies/DELETE|Beleid verwijderen|
|/vaults/replicationRecoveryPlans/Read|Alle herstelplannen lezen|
|/vaults/replicationRecoveryPlans/Write|Maken of bijwerken van een herstelplannen|
|/vaults/replicationRecoveryPlans/DELETE|Verwijderen van eventuele herstelplannen|
|/vaults/replicationRecoveryPlans/plannedFailover/Action|Plan voor herstel voor geplande Failover|
|/vaults/replicationRecoveryPlans/unplannedFailover/Action|Plan voor herstel van failover|
|/vaults/replicationRecoveryPlans/testFailover/Action|Test Failover herstelplan|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/Action|Test het opruimen van herstelplan|
|/vaults/replicationRecoveryPlans/failoverCommit/Action|Herstelplan-failover doorvoeren|
|/vaults/replicationRecoveryPlans/reProtect/Action|Plan voor herstel opnieuw beveiligen|
|Kluizen/extendedInformation/leestijd|Hallo uitgebreide Info ophalen bewerking opgehaald van een object uitgebreid Info hello Azure-resource van het type dat vertegenwoordigt? kluis?|
|Kluizen/extendedInformation/schrijftijd|Hallo uitgebreide Info ophalen bewerking opgehaald van een object uitgebreid Info hello Azure-resource van het type dat vertegenwoordigt? kluis?|
|/ Kluizen/extendedInformation/verwijderen|Hallo uitgebreide Info ophalen bewerking opgehaald van een object uitgebreid Info hello Azure-resource van het type dat vertegenwoordigt? kluis?|
|Kluizen/backupManagementMetaData/leestijd|Hiermee worden de metagegevens van back-upbeheer voor een Recovery Services-kluis geretourneerd.|
|Kluizen/backupProtectionContainers/leestijd|Retourneert alle containers behoren toohello abonnement|
|Kluizen/backupFabrics/operationResults/leestijd|Retourneert de status van Hallo-bewerking|
|Kluizen/backupFabrics/protectionContainers/leestijd|Retourneert alle geregistreerde containers|
|/ Kluizen/backupFabrics/protectionContainers /<br>operationResults leestijd|Hiermee wordt het resultaat opgehaald van de bewerking die is uitgevoerd op de beveiligde container.|
|/ Kluizen/backupFabrics/protectionContainers /<br>protectedItems leestijd|Geeft de details van Hallo beveiligd Item object|
|/ Kluizen/backupFabrics/protectionContainers /<br>protectedItems/schrijven|Een back-up beveiligd Item maken|
|/ Kluizen/backupFabrics/protectionContainers /<br>protectedItems/verwijderen|Hiermee verwijdert u beveiligd Item|
|/ Kluizen/backupFabrics/protectionContainers /<br>back-up-protectedItems/actie|Hiermee wordt een back-up van het beveiligde item gemaakt.|
|/ Kluizen/backupFabrics/protectionContainers /<br>operationResults protectedItems leestijd|Hiermee wordt het resultaat opgehaald van de bewerking die is uitgevoerd op beveiligde items.|
|/ Kluizen/backupFabrics/protectionContainers /<br>operationStatus protectedItems leestijd|Retourneert Hallo status van de bewerking uitgevoerd op beveiligde Items.|
|/ Kluizen/backupFabrics/protectionContainers /<br>recoveryPoints protectedItems leestijd|Herstelpunten voor beveiligde items ophalen.|
|/ Kluizen/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>/ herstelbewerking|Herstelpunten voor beveiligde items herstellen.|
|/ Kluizen/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>provisionInstantItemRecovery/actie|Inrichten Instant Item herstel voor beveiligde Item|
|/ Kluizen/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>revokeInstantItemRecovery/actie|Herstel op directe intrekken voor beveiligde Item|
|Kluizen/gebruik/leestijd|Hiermee worden de gebruiksgegevens voor een Recovery Services-kluis geretourneerd.|
|/vaults/usages/Read|Lezen van het gebruik van een kluis|
|Kluizen/certificaten/schrijftijd|Hallo bewerking Update Resource certificaat updates Hallo resource/kluis referenties van het certificaat.|
|Kluizen/tokenInfo/leestijd|Retourneert token-informatie voor de Recovery Services-kluis.|
|/vaults/replicationAlertSettings/Read|Alle instellingen voor waarschuwingen lezen|
|/vaults/replicationAlertSettings/Write|Alle waarschuwingsinstellingen maken of bijwerken|
|Kluizen/backupOperations/leestijd|Back-upbewerking retourneert Status voor de Recovery Services-kluis.|
|Kluizen/storageConfig/leestijd|Retourneert opslagconfiguratie voor Recovery Services-kluis.|
|Kluizen/storageConfig/schrijftijd|De opslagconfiguratie updates voor Recovery Services-kluis.|
|Kluizen/backupUsageSummaries/leestijd|Samenvattingen retourneert voor beveiligde Items en beveiligde Servers voor een Recovery Services.|
|Kluizen/backupProtectedItems/leestijd|Retourneert Hallo lijst met alle beveiligde Items.|
|Kluizen/backupconfig/vaultconfig/leestijd|Retourneert-configuratie voor Recovery Services-kluis.|
|Kluizen/backupconfig/vaultconfig/schrijftijd|Configuratie van de updates voor Recovery Services-kluis.|
|Kluizen/registeredIdentities/schrijftijd|Hallo servicecontainer registreren bewerking mag gebruikte tooregister een container met Service voor herstel.|
|Kluizen/registeredIdentities/leestijd|Hallo ophalen Containers bewerking kan worden gebruikt ophalen Hallo-containers die zijn geregistreerd voor een resource.|
|/ Kluizen/registeredIdentities/verwijderen|Hallo Container registratie-bewerking kan worden gebruikt toounregister een container.|
|Kluizen/registeredIdentities/operationResults/leestijd|Hallo Bewerkingsresultaten ophalen bewerking kan worden gebruikt get Hallo bewerkingsstatus en ertoe leiden dat Hallo asynchroon opnieuw ingediend|
|/vaults/replicationJobs/Read|Lezen van taken|
|/vaults/replicationJobs/Cancel/Action|Taak annuleren|
|/vaults/replicationJobs/restart/Action|Taak opnieuw starten|
|/vaults/replicationJobs/Resume/Action|Taak hervatten|
|Kluizen/backupPolicies/leestijd|Retourneert alle beleidsregels voor beveiliging|
|Kluizen/backupPolicies/schrijftijd|Hiermee maakt u het beveiligingsbeleid|
|/ Kluizen/backupPolicies/verwijderen|Een beveiligingsbeleid voor verwijderen|
|Kluizen/backupPolicies/operationResults/leestijd|Hiermee worden de resultaten van de beleidsbewerking opgehaald.|
|Kluizen/backupPolicies/operationStatus/leestijd|Status van de beleidsbewerking ophalen.|
|Kluizen/vaultTokens/leestijd|Hallo kluis Token opnieuw kan worden gebruikt tooget kluis Token voor kluis niveau back-end-bewerkingen.|
|Kluizen/monitoringConfigurations/notificationConfiguration/leestijd|Hiermee haalt u Meldingsconfiguratie voor Hallo Recovery services-kluis.|
|Kluizen/backupJobs/leestijd|Retourneert alle objecten van de taak|
|/ Kluizen/backupJobs / / actie voor annuleren|Hallo taak annuleren|
|Kluizen/backupJobs/operationResults/leestijd|Retourneert hello resultaat Job-bewerking.|
|/Locations/allocateStamp/Action|AllocateStamp is een interne bewerking die wordt gebruikt door de service|
|/Locations/allocatedStamp/Read|GetAllocatedStamp is een interne bewerking die wordt gebruikt door de service|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Bewerking | Beschrijving |
|---|---|
|/ checkNamespaceAvailability/actie|Hiermee wordt de beschikbaarheid van de naamruimte in een bepaald abonnement gecontroleerd.|
|registratie-/ actie|Hallo-abonnement voor Hallo Relay resourceprovider registreert en wordt Hallo maken van de Relay-resources|
|naamruimten/schrijven|Een Namespace-Resource maken en bijwerken van de eigenschappen ervan. Tags en status van Hallo Namespace zijn Hallo-eigenschappen die kunnen worden bijgewerkt.|
|/Namespaces/Read|Hallo-lijst van Namespace resourcebeschrijving ophalen|
|/ naamruimten/verwijderen|Namespace-bron verwijderen|
|/Namespaces/authorizationRules/Write|Een Namespace niveau autorisatieregels maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/authorizationRules/DELETE|Namespace autorisatieregel verwijderen. Hallo Namespace autorisatie standaardregel kan niet worden verwijderd. |
|/Namespaces/authorizationRules/listkeys/Action|Hallo verbindingsreeks toohello Namespace ophalen|
|/Namespaces/HybridConnections/Write|Maken of bijwerken HybridConnection eigenschappen.|
|/Namespaces/HybridConnections/Read|Lijst met beschrijvingen van de Resource HybridConnection ophalen|
|/Namespaces/HybridConnections/DELETE|Bewerking toodelete HybridConnection Resource|
|/Namespaces/HybridConnections/authorizationRules/Write|Autorisatieregels HybridConnection maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/HybridConnections/authorizationRules/DELETE|Bewerking toodelete HybridConnection autorisatieregels|
|/Namespaces/HybridConnections/authorizationRules/listkeys/Action|Hallo verbindingsreeks tooHybridConnection ophalen|
|/Namespaces/WcfRelays/Write|Maken of bijwerken WcfRelay eigenschappen.|
|/Namespaces/WcfRelays/Read|Lijst met beschrijvingen van de Resource WcfRelay ophalen|
|/Namespaces/WcfRelays/DELETE|Bewerking toodelete WcfRelay Resource|
|/Namespaces/WcfRelays/authorizationRules/Write|Autorisatieregels WcfRelay maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/WcfRelays/authorizationRules/DELETE|Bewerking toodelete WcfRelay autorisatieregels|
|/Namespaces/WcfRelays/authorizationRules/listkeys/Action|Hallo verbindingsreeks tooWcfRelay ophalen|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Bewerking | Beschrijving |
|---|---|
|AvailabilityStatuses/leestijd|Opgehaald Hallo beschikbaarheid statussen voor alle resources in Hallo opgegeven bereik|
|AvailabilityStatuses/current/leestijd|Opgehaald Hallo beschikbaarheidsstatus voor Hallo van de opgegeven bron|

## <a name="microsoftresources"></a>Microsoft.Resources

| Bewerking | Beschrijving |
|---|---|
|/ checkResourceName/actie|Controleer Hallo resourcenaam geldig.|
|/providers/Read|Hallo-lijst met providers ophalen.|
|/Subscriptions/Read|Hallo-lijst met abonnementen ophalen.|
|/Subscriptions/operationresults/Read|Hallo abonnement Bewerkingsresultaten ophalen.|
|/Subscriptions/providers/Read|Hiermee kunt u de resourceproviders ophalen of opnemen in een lijst.|
|/Subscriptions/tagNames/Read|Hiermee kunt u abonnementslabels ophalen of opnemen in een lijst.|
|/Subscriptions/tagNames/Write|Hiermee kunt u een abonnementslabel toevoegen.|
|/Subscriptions/tagNames/DELETE|Hiermee kunt u een abonnementslabel verwijderen.|
|/Subscriptions/tagNames/tagValues/Read|Hiermee kunt u abonnementslabelwaarden ophalen of opnemen in een lijst.|
|/Subscriptions/tagNames/tagValues/Write|Hiermee kunt u een abonnementslabelwaarde toevoegen.|
|/Subscriptions/tagNames/tagValues/DELETE|Hiermee kunt een abonnementslabelwaarde verwijderen.|
|/subscriptions/resources/Read|Hiermee kunt u de resources van een abonnement ophalen.|
|/Subscriptions/resourceGroups/Read|Hiermee kunt u resourcegroepen ophalen of opnemen in een lijst.|
|/Subscriptions/resourceGroups/Write|Hiermee kunt u een resourcegroep maken of bijwerken.|
|/Subscriptions/resourceGroups/DELETE|Hiermee kunt u een resourcegroep en de bijhorende resources verwijderen.|
|/Subscriptions/resourceGroups/moveResources/Action|Bronnen verplaatst van één resource groep tooanother.|
|/Subscriptions/resourceGroups/validateMoveResources/Action|Verplaatsing van resources van één resource groep tooanother valideren.|
|/Subscriptions/ResourceGroups/resources/Read|Hallo-resources voor de resourcegroep Hallo opgehaald.|
|/Subscriptions/ResourceGroups/Deployments/Read|Hiermee kunt u implementaties ophalen of opnemen in een lijst.|
|/Subscriptions/ResourceGroups/Deployments/Write|Hiermee kunt u een implementatie maken of bijwerken.|
|/Subscriptions/ResourceGroups/Deployments/operationstatuses/Read|Hiermee kunt u of implementatie bewerking statussen.|
|/Subscriptions/ResourceGroups/Deployments/Operations/Read|Hiermee kunt u implementatiebewerkingen ophalen of opnemen in een lijst.|
|/Subscriptions/Locations/Read|Hallo-lijst met ondersteunde locaties ophalen.|
|/links/Read|Hiermee kunt u resourcekoppelingen ophalen of opnemen in een lijst.|
|koppelingen/schrijven|Hiermee kunt u een resourcekoppeling maken of bijwerken.|
|/links/DELETE|Hiermee kunt u een resourcekoppeling verwijderen.|
|/tenants/Read|Hallo-lijst met tenants ophalen.|
|/resources/Read|Hallo-lijst met resources op basis van filters opgehaald.|
|/Deployments/Read|Hiermee kunt u implementaties ophalen of opnemen in een lijst.|
|implementaties van/schrijven|Hiermee kunt u een implementatie maken of bijwerken.|
|/Deployments/DELETE|Hiermee kunt u een implementatie verwijderen.|
|/Deployments/Cancel/Action|Hiermee kunt u een implementatie annuleren.|
|/Deployments/Validate/Action|Hiermee kunt u een implementatie valideren.|
|/Deployments/Operations/Read|Hiermee kunt u implementatiebewerkingen ophalen of opnemen in een lijst.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Bewerking | Beschrijving |
|---|---|
|/jobcollections/Read|Taakverzameling ophalen|
|taakverzamelingen/schrijven|Hiermee maakt u een taakverzameling of werkt u er een bij.|
|/jobcollections/DELETE|Hiermee verwijdert u de taakverzameling.|
|/jobcollections/Enable/Action|Kan taakverzameling.|
|/jobcollections/Disable/Action|Taakverzameling wordt uitgeschakeld.|
|/jobcollections/Jobs/Read|Taak opgehaald.|
|/jobcollections/Jobs/Write|Hiermee maakt u een taak of werkt u er een bij.|
|/jobcollections/Jobs/DELETE|Hiermee verwijdert u een taak.|
|/jobcollections/Jobs/Run/Action|De taak wordt uitgevoerd.|
|/jobcollections/Jobs/generateLogicAppDefinition/Action|Hiermee wordt een definitie voor een logische app gegenereerd op basis van een Scheduler-taak.|
|/jobcollections/Jobs/jobhistories/Read|Taakgeschiedenis opgehaald.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo-abonnement van de resource zoekmachine Hallo registreert en wordt Hallo maken van de search-services.|
|/ checkNameAvailability/actie|Controleert de beschikbaarheid van de servicenaam Hallo.|
|searchServices/schrijven|Maken of bijwerken van Hallo search-service.|
|/searchServices/Read|Hallo search-service worden gelezen.|
|/searchServices/DELETE|Hiermee verwijdert u Hallo search-service.|
|/searchServices/start/Action|Hallo search-service start.|
|/searchServices/Stop/Action|Hallo search-service stopt.|
|/searchServices/listAdminKeys/Action|Hallo beheerder sleutels leest.|
|/searchServices/regenerateAdminKey/Action|Hallo beheerder sleutel genereert.|
|/searchServices/createQueryKey/Action|Hallo-querysleutel maakt.|
|/searchServices/queryKey/Read|Hallo querysleutels leest.|
|/searchServices/queryKey/DELETE|Hiermee verwijdert u Hallo querysleutel.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Bewerking | Beschrijving |
|---|---|
|/jitNetworkAccessPolicies/Read|Hallo just in time netwerktoegangsbeleid opgehaald|
|jitNetworkAccessPolicies/schrijven|Hiermee maakt u een nieuw netwerk just-in-time-beleid of een bestaande bijgewerkt|
|/jitNetworkAccessPolicies/initiate/Action|Initieert een netwerktoegangsbeleid just in time|
|/securitySolutionsReferenceData/Read|Hallo beveiligingsoplossingen referentiegegevens opgehaald|
|/securityStatuses/Read|Hallo beveiliging van health-statussen voor Azure-resources opgehaald|
|/webApplicationFirewalls/Read|Hallo web application firewalls opgehaald|
|webApplicationFirewalls/schrijven|Hiermee maakt u een nieuwe web application firewall of een bestaande bijgewerkt|
|/webApplicationFirewalls/DELETE|Hiermee verwijdert u een web application firewall|
|/securitySolutions/Read|Hallo beveiligingsoplossingen opgehaald|
|securitySolutions/schrijven|Maakt een nieuwe beveiligingsoplossing of een bestaande bijgewerkt|
|/securitySolutions/DELETE|Hiermee verwijdert u een beveiligingsoplossing|
|/Tasks/Read|Alle beschikbare beveiligingsaanbevelingen opgehaald|
|/Tasks/Dismiss/Action|Een beveiligingsaanbeveling negeren|
|/Tasks/Activate/Action|Een beveiligingsaanbeveling activeren|
|/Policies/Read|Hallo-beveiligingsbeleid opgehaald|
|/ beleid/schrijven|Updates Hallo beveiligingsbeleid|
|/applicationWhitelistings/Read|Hallo toepassing whitelistings opgehaald|
|applicationWhitelistings/schrijven|Hiermee maakt u een nieuwe toepassing whitelisting of een bestaande bijgewerkt|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Bewerking | Beschrijving |
|---|---|
|/ subscriptions/schrijven|Maken of bijwerken van een abonnement|
|gateways/schrijven|Maken of bijwerken van een gateway|
|/gateways/DELETE|Hiermee verwijdert u een gateway|
|/gateways/Read|Een gateway opgehaald|
|/gateways/regenerateprofile/Action|Hallo gateway profiel wordt opnieuw gegenereerd|
|/gateways/upgradetolatest/Action|Upgrades Hallo gateway toohello meest recente versie|
|knooppunten/schrijven|maken of bijwerken van een knooppunt|
|/nodes/DELETE|Hiermee verwijdert u een knooppunt|
|/nodes/Read|Een knooppunt opgehaald|
|sessies/schrijven|Maken of bijwerken van een sessie|
|/Sessions/Read|Een sessie opgehaald|
|/Sessions/DELETE|Hiermee verwijdert u een sesssion|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Bewerking | Beschrijving |
|---|---|
|/ checkNameAvailability/actie|Hiermee wordt de beschikbaarheid van de naamruimte in een bepaald abonnement gecontroleerd.|
|registratie-/ actie|Hallo-abonnement voor Hallo ServiceBus-resourceprovider geregistreerd en kunnen Hallo maken van service bus-resources|
|naamruimten/schrijven|Een Namespace-Resource maken en bijwerken van de eigenschappen ervan. Tags en status van Hallo Namespace zijn Hallo-eigenschappen die kunnen worden bijgewerkt.|
|/Namespaces/Read|Hallo-lijst van Namespace resourcebeschrijving ophalen|
|/ naamruimten/verwijderen|Namespace-bron verwijderen|
|/Namespaces/metricDefinitions/Read|Lijst met Namespace metrische Resource beschrijvingen|
|/Namespaces/authorizationRules/Write|Een Namespace niveau autorisatieregels maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/authorizationRules/Read|Hallo-lijst van de beschrijving van de naamruimten autorisatieregels ophalen.|
|/Namespaces/authorizationRules/DELETE|Namespace autorisatieregel verwijderen. Hallo Namespace autorisatie standaardregel kan niet worden verwijderd. |
|/Namespaces/authorizationRules/listkeys/Action|Hallo verbindingsreeks toohello Namespace ophalen|
|/Namespaces/authorizationRules/regenerateKeys/Action|Hallo primaire of secundaire sleutel toohello Resource genereren|
|/Namespaces/diagnosticSettings/Read|Lijst met beschrijvingen van de Resource Namespace diagnostische instellingen|
|/Namespaces/diagnosticSettings/Write|Lijst met beschrijvingen van de Resource Namespace diagnostische instellingen|
|/Namespaces/Queues/Write|Maken of wachtrijeigenschappen Update.|
|/Namespaces/Queues/Read|Lijst met beschrijvingen van de wachtrij-Resource|
|/Namespaces/Queues/DELETE|Bewerking toodelete Queue-bron|
|/Namespaces/Queues/authorizationRules/Write|Autorisatieregels wachtrij maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/Queues/authorizationRules/Read| Hallo-lijst van autorisatieregels wachtrij ophalen|
|/Namespaces/Queues/authorizationRules/DELETE|Bewerking toodelete wachtrij-autorisatieregels|
|/Namespaces/Queues/authorizationRules/listkeys/Action|Hallo verbindingsreeks tooQueue ophalen|
|/Namespaces/Queues/authorizationRules/regenerateKeys/Action|Hallo primaire of secundaire sleutel toohello Resource genereren|
|/Namespaces/logDefinitions/Read|Lijst met Namespace logboeken Resource beschrijvingen|
|/Namespaces/Topics/Write|Maken of bijwerken onderwerp eigenschappen.|
|/Namespaces/Topics/Read|Lijst met beschrijvingen van de Resource onderwerp|
|/Namespaces/Topics/DELETE|Bewerking toodelete onderwerp Resource|
|/Namespaces/Topics/authorizationRules/Write|Verificatieregels onderwerp maken en bijwerken van de eigenschappen ervan. Hallo autorisatie regels toegangsrechten, Hallo primaire en secundaire sleutels kunnen worden bijgewerkt.|
|/Namespaces/Topics/authorizationRules/Read| Hallo-lijst met verificatieregels onderwerp|
|/Namespaces/Topics/authorizationRules/DELETE|Bewerking toodelete verificatieregels onderwerp|
|/Namespaces/Topics/authorizationRules/listkeys/Action|Hallo verbindingsreeks tooTopic ophalen|
|/Namespaces/Topics/authorizationRules/regenerateKeys/Action|Hallo primaire of secundaire sleutel toohello Resource genereren|
|/Namespaces/Topics/Subscriptions/Write|Maken of bijwerken TopicSubscription eigenschappen.|
|/Namespaces/Topics/Subscriptions/Read|Lijst met beschrijvingen van de Resource TopicSubscription ophalen|
|/Namespaces/Topics/Subscriptions/DELETE|Bewerking toodelete TopicSubscription Resource|
|/Namespaces/Topics/Subscriptions/Rules/Write|Maken of de eigenschappen van de regel voor het bijwerken.|
|/Namespaces/Topics/Subscriptions/Rules/Read|Lijst met beschrijvingen van de Resource regel|
|/Namespaces/Topics/Subscriptions/Rules/DELETE|Bewerking toodelete regel Resource|

## <a name="microsoftsql"></a>Microsoft.Sql

| Bewerking | Beschrijving |
|---|---|
|/servers/Read|Retourneert een lijst met servers in een resourcegroep voor een abonnement|
|servers/schrijven|Maak een nieuwe server of de eigenschappen van bestaande server in een resourcegroep voor een abonnement wijzigen|
|/servers/DELETE|Verwijderen van een server en alle ingesloten databases en elastische pools|
|/servers/import/Action|Een nieuwe database op Hallo server maken en implementeren van schema en de gegevens uit een DacPac-pakket|
|/servers/upgrade/Action|Nieuwe functionaliteit die beschikbaar zijn op de meest recente versie Hallo van server inschakelen en databases edition conversie-kaart|
|/servers/VulnerabilityAssessmentScans/Action|Server-scan voor beoordeling van beveiligingsproblemen uitvoeren|
|/servers/operationResults/Read|Bewerking wordt gebruikt tootrack voortgang van de upgrade van de server van een lagere versie toohigher|
|/servers/operationResults/DELETE|Upgrade van versie server bezig afbreken|
|/servers/securityAlertPolicies/Read|Details van Hallo server threat detectie beleid zijn geconfigureerd op een bepaalde server ophalen|
|/servers/securityAlertPolicies/Write|Hallo-server de detectie van dreigingen voor een bepaalde server wijzigen|
|/servers/securityAlertPolicies/operationResults/Read|Resultaten van de detectie van dreigingen beleid Set-bewerking voor het Hallo-server ophalen|
|/servers/Administrators/Read|Administrator-servergegevens ophalen|
|/servers/Administrators/Write|Maken of bijwerken van de serverbeheerder|
|/servers/Administrators/DELETE|Server-beheerder van Hallo server verwijderen|
|/servers/recoverableDatabases/Read|Deze bewerking wordt gebruikt voor herstel na noodgevallen van actieve database toorestore database toolast bekende goede back-punt. Gegevens over Hallo laatste goede back-up worden geretourneerd, maar deze niet daadwerkelijk Hallo-database herstelt.|
|/servers/serviceObjectives/Read|Lijst met serviceniveaudoelstellingen (ook wel bekend als prestatielagen) beschikbaar is op een bepaalde server ophalen|
|/servers/firewallRules/Read|Firewall-regel servergegevens ophalen|
|/servers/firewallRules/Write|Server firewall-regel waarmee de IP-adresbereik toegestaan tooconnect toohello server maken of bijwerken|
|/servers/firewallRules/DELETE|Firewallregel van Hallo server verwijderen|
|/servers/administratorOperationResults/Read|Ophalen van server-beheerder Bewerkingsresultaten|
|/servers/recommendedElasticPools/Read|Aanbevelingen voor elastische pools tooreduce databasekosten ophalen of de prestaties op basis van Resourcegebruik historica verbeteren|
|/servers/recommendedElasticPools/metrics/Read|Metrische gegevens voor aanbevolen elastische databases voor een bepaalde server ophalen|
|/servers/recommendedElasticPools/databases/Read|Ophalen van databases die moeten worden toegevoegd aan het aanbevolen pools voor elastische databases voor een bepaalde server|
|/servers/elasticPools/Read|Ophalen van gegevens van de pool voor elastische database op een bepaalde server|
|/servers/elasticPools/Write|Maak een nieuwe eigenschappen of wijzigen van bestaande pool voor elastische database|
|/servers/elasticPools/DELETE|Verwijderen van bestaande pool voor elastische database|
|/servers/elasticPools/operationResults/Read|Ophalen van gegevens op een bewerking van de groep van toepassingen opgegeven elastische database|
|/servers/elasticPools/providers/Microsoft.Insights/<br>metricDefinitions leestijd|Retourtypen van metrische gegevens die beschikbaar voor pools voor elastische databases zijn|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings leestijd|Hallo diagnostische instelling voor Hallo-resource opgehaald|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/schrijven|Maken of bijwerken van diagnostische instelling voor de resource Hallo Hallo|
|/servers/elasticPools/metrics/Read|Gebruik van metrische gegevens voor elastische database groep resources retourneren|
|/servers/elasticPools/elasticPoolDatabaseActivity/Read|Ophalen van activiteiten en meer informatie over een bepaalde database die deel uitmaakt van een pool voor elastische database|
|/servers/elasticPools/Advisors/Read|Lijst met adviseurs die beschikbaar zijn voor de elastische groep Hallo retourneert|
|/servers/elasticPools/Advisors/Write|Update automatisch-execute status van een advisor op niveau van de elastische groep.|
|/servers/elasticPools/Advisors/recommendedActions/Read|Lijst met aanbevolen acties van opgegeven advisor voor de elastische groep Hallo retourneert|
|/servers/elasticPools/Advisors/recommendedActions/Write|Aanbevolen actie op de elastische groep Hallo Hallo toepassen|
|/servers/elasticPools/elasticPoolActivity/Read|Ophalen van activiteiten en meer informatie over een bepaalde elastische databasegroep|
|/servers/elasticPools/databases/Read|Ophalen van de lijst en details van de databases die deel van een pool voor elastische database op een bepaalde server uitmaken|
|/servers/auditingPolicies/Read|Ophalen van gegevens van Hallo server standaardtabel controlebeleid geconfigureerd op een bepaalde server|
|/servers/auditingPolicies/Write|Hallo servertabel met standaardtijden voor controle-instellingen voor een bepaalde server wijzigen|
|/servers/disasterRecoveryConfiguration/operationResults/Read|Disaster Recovery configuratie Bewerkingsresultaten ophalen|
|/servers/Advisors/Read|Retourneert de lijst met adviseurs beschikbaar voor Hallo-server|
|/servers/Advisors/Write|Updates execute automatisch-status van een advisor op serverniveau.|
|/servers/Advisors/recommendedActions/Read|Retourneert de lijst met aanbevolen acties van opgegeven advisor voor Hallo-server|
|/servers/Advisors/recommendedActions/Write|Aanbevolen actie op de server Hallo Hallo toepassen|
|/servers/usages/Read|DTU-quotum voor server en de huidige DTU consuption geretourneerd door alle databases binnen Hallo-server|
|/servers/elasticPoolEstimates/Read|Retourneert de lijst van de elastische groep schattingen al is gemaakt voor deze server|
|/servers/elasticPoolEstimates/Write|Hiermee maakt u nieuwe elastische pool schatting voor de lijst met databases die zijn opgegeven|
|/servers/auditingSettings/Read|Ophalen van gegevens van Hallo server blob controlebeleid geconfigureerd op een bepaalde server|
|/servers/auditingSettings/Write|Hallo server auditingfunctie voor blobs voor een bepaalde server wijzigen|
|/servers/auditingSettings/operationResults/Read|Resultaat van Hallo server blob controle beleid Set-bewerking ophalen|
|/servers/backupLongTermRetentionVaults/Read|Deze bewerking is gebruikte tooget een back-up langdurig bewaren kluis. Gegevens over Hallo kluis geregistreerde toothis server worden geretourneerd.|
|/servers/backupLongTermRetentionVaults/Write|Een back-up langdurig bewaren kluis registreren|
|/servers/restorableDroppedDatabases/Read|Een lijst met databases die zijn verwijderd op een bepaalde server die binnen het bewaarbeleid ophalen. Deze bewerking wordt een lijst van databases en gekoppelde metagegevens, zoals de datum van verwijdering.|
|/servers/databases/Read|Retourneert een lijst met servers in een resourcegroep voor een abonnement|
|/servers/databases/Write|Maak een nieuwe server of de eigenschappen van bestaande server in een resourcegroep voor een abonnement wijzigen|
|/servers/databases/DELETE|Verwijderen van een server en alle ingesloten databases en elastische pools|
|/servers/databases/export/Action|Een nieuwe database op Hallo server maken en implementeren van schema en de gegevens uit een DacPac-pakket|
|/servers/databases/VulnerabilityAssessmentScans/Action|Database-scan voor beoordeling van beveiligingsproblemen worden uitgevoerd.|
|/servers/databases/pause/Action|Onderbreken van een DataWarehouse-database|
|/servers/databases/Resume/Action|Een DataWarehouse-editie database hervatten|
|/servers/databases/operationResults/Read|Bewerking wordt gebruikt tootrack voortgang van langdurige databasebewerking, zoals de schaal.|
|/servers/databases/replicationLinks/Read|Geretourneerde gegevens over koppelingen voor databasereplicatie tot stand gebracht voor een bepaalde database|
|/servers/databases/replicationLinks/DELETE|Beëindigen van de replicatierelatie Hallo geforceerd en met mogelijk gegevensverlies|
|/servers/databases/replicationLinks/Unlink/Action|Hallo replicatierelatie beëindigen geforceerd of na het synchroniseren met Hallo partner|
|/servers/databases/replicationLinks/failover/Action|Failover na het synchroniseren van alle wijzigingen van Hallo primaire, waardoor deze database in Hallo replicatierelatie primaire en aanbrengen Hallo externe primaire naar een secundair|
|/servers/databases/replicationLinks/forceFailoverAllowDataLoss/Action|Failover onmiddellijk met mogelijk gegevensverlies, waardoor deze database in Hallo replicatierelatie Hallo van primaire en die extern primaire naar een secundair|
|/servers/databases/replicationLinks/updateReplicationMode/Action|Replicatiemodus voor koppeling toosynchronous of asynchrone modus bijwerken|
|/servers/databases/replicationLinks/operationResults/Read|Status van langlopende bewerkingen op de koppelingen voor databasereplicatie ophalen|
|/servers/databases/dataMaskingPolicies/Read|Ophalen van gegevens van het beleid dat is geconfigureerd op een bepaalde database maskeren Hallo van gegevens|
|/servers/databases/dataMaskingPolicies/Write|Beleid voor een bepaalde database gegevensmaskering wijzigen|
|/servers/databases/dataMaskingPolicies/Rules/Read|Ophalen van gegevens van het maskeren van de beleidsregel die zijn geconfigureerd op een bepaalde database Hallo van gegevens|
|/servers/databases/dataMaskingPolicies/Rules/Write|Gegevensmaskering beleidsregel voor een bepaalde database wijzigen|
|/servers/databases/securityAlertPolicies/Read|Ophalen van gegevens van Hallo threat detectie beleid zijn geconfigureerd op een bepaalde database|
|/servers/databases/securityAlertPolicies/Write|Hallo threat detectie beleid voor een bepaalde database wijzigen|
|/servers/databases/providers/Microsoft.Insights/<br>metricDefinitions leestijd|Retourtypen van metrische gegevens die beschikbaar voor databases zijn|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings leestijd|Hallo diagnostische instelling voor Hallo-resource opgehaald|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/schrijven|Maken of bijwerken van diagnostische instelling voor de resource Hallo Hallo|
|/servers/databases/providers/Microsoft.Insights/<br>logDefinitions leestijd|Hallo beschikbare logboeken opgehaald voor databases|
|/servers/databases/topQueries/Read|Retourneert geaggregeerd runtime-statistieken voor de geselecteerde query in de geselecteerde tijdsperiode|
|/servers/databases/topQueries/queryText/Read|Retourneert Hallo Transact-SQL-tekst voor de geselecteerde query-ID|
|/servers/databases/topQueries/statistics/Read|Retourneert geaggregeerd runtime-statistieken voor de geselecteerde query in de geselecteerde tijdsperiode|
|/servers/databases/connectionPolicies/Read|Ophalen van gegevens van Hallo verbindingsbeleid geconfigureerd op een bepaalde database|
|/servers/databases/connectionPolicies/Write|Verbindingsbeleid voor een bepaalde database wijzigen|
|/servers/databases/metrics/Read|Metrische gegevens voor het gebruik van database resources retourneren|
|/servers/databases/auditRecords/Read|Hallo database blob controlerecords ophalen|
|/servers/databases/transparentDataEncryption/Read|Status en details van transparent data encryption beveiligingsfunctie voor een bepaalde database ophalen|
|/servers/databases/transparentDataEncryption/Write|In- of uitschakelen van transparante gegevensversleuteling voor een bepaalde database|
|/servers/databases/transparentDataEncryption/operationResults/Read|Status en details van transparent data encryption beveiligingsfunctie voor een bepaalde database ophalen|
|/servers/databases/auditingPolicies/Read|Ophalen van gegevens van Hallo tabel controlebeleid geconfigureerd op een bepaalde database|
|/servers/databases/auditingPolicies/Write|Hallo tabel controlebeleid voor een bepaalde database wijzigen|
|/servers/databases/dataWarehouseQueries/Read|Retourneert Hallo datawarehouse distributie query-gegevens voor geselecteerde query-ID|
|servers/databases/dataWarehouseQueries /<br>dataWarehouseQuerySteps leestijd|Retourneert Hallo gedistribueerde query stap informatie van datawarehouse-query voor de geselecteerde stap-ID|
|/servers/databases/serviceTierAdvisors/Read|Retourneren van suggestie over het schalen van database omhoog of omlaag op basis van de prestaties van query's uitvoeren statistieken tooimprove of kosten|
|/servers/databases/Advisors/Read|Lijst met adviseurs beschikbaar voor de database Hallo retourneert|
|/servers/databases/Advisors/Write|Update automatisch-execute status van een advisor op databaseniveau.|
|/servers/databases/Advisors/recommendedActions/Read|Retourneert de lijst met aanbevolen acties van de opgegeven advisor voor Hallo-database|
|/servers/databases/Advisors/recommendedActions/Write|Aanbevolen actie voor de database Hallo Hallo toepassen|
|/servers/databases/usages/Read|Maximale databasegrootte die kan worden bereikt en de huidige grootte bezet door gegevens worden geretourneerd|
|/servers/databases/queryStore/Read|Retourneert de huidige waarden van instellingen voor database Hallo Query Store|
|/servers/databases/queryStore/Write|Query Store-instelling voor de database Hallo-updates|
|/servers/databases/auditingSettings/Read|Ophalen van gegevens van Hallo blob controlebeleid geconfigureerd op een bepaalde database|
|/servers/databases/auditingSettings/Write|Hallo blob controlebeleid voor een bepaalde database wijzigen|
|/servers/databases/schemas/Tables/recommendedIndexes/Read|Lijst met indexaanbevelingen voor een database ophalen|
|/servers/databases/schemas/Tables/recommendedIndexes/Write|Indexaanbeveling toepassen|
|/servers/databases/schemas/Tables/Columns/Read|Ophalen van lijst met kolommen van een tabel|
|/servers/databases/missingindexes/Read|Suggesties over database-indexen toocreate retourneren, wijzigen of verwijderen in de volgorde tooimprove query-prestaties|
|/servers/databases/missingindexes/Write|Database-indexaanbeveling in een bepaalde database gebruiken|
|/servers/databases/importExportOperationResults/Read|Details over het importeren van de database- of exportbewerking uit DacPac zich in de storage-account|
|/servers/importExportOperationResults/Read|Lijst met details voor de database importbewerkingen Hallo retourneren uit storage-account op een bepaalde server|

## <a name="microsoftstorage"></a>Microsoft.Storage

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Hallo-abonnement voor Hallo opslagresourceprovider geregistreerd en Hallo maken van opslagaccounts maakt.|
|/checknameavailability/Read|Hiermee controleert u of een accountnaam geldig is en niet wordt gebruikt.|
|storageAccounts/schrijven|Maakt een opslagaccount met Hallo opgegeven parameters of update voegt de aangepaste eigenschappen of labels Hallo domein voor Hallo storage-account opgegeven.|
|/storageAccounts/DELETE|Hiermee verwijdert u een bestaand opslagaccount.|
|/storageAccounts/listkeys/Action|Retourneert Hallo toegangstoetsen voor Hallo opgegeven storage-account.|
|/storageAccounts/regeneratekey/Action|Opnieuw Hallo toegangstoetsen voor Hallo opgegeven storage-account.|
|/storageAccounts/Read|Retourneert Hallo lijst met opslagaccounts of haalt Hallo eigenschappen voor Hallo storage-account opgegeven.|
|/storageAccounts/listAccountSas/Action|Retourneert Hallo Account-SAS-token voor Hallo opgegeven storage-account.|
|/storageAccounts/listServiceSas/Action|Storage-Service-SAS-Token|
|/storageAccounts/Services/diagnosticSettings/Write|Diagnostische instellingen voor storage-account maken of bijwerken.|
|/skus/Read|Een lijst met hello SKU's die worden ondersteund door Microsoft.Storage.|
|/usages/Read|Retourneert de limiet Hallo en het huidige gebruik aantal Hallo voor resources in Hallo opgegeven abonnement|
|/Operations/Read|Polls Hallo status van een asynchrone bewerking.|
|/Locations/deleteVirtualNetworkOrSubnets/Action|Microsoft.Storage waarschuwt dat virtuele netwerk of subnet wordt verwijderd|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Bewerking | Beschrijving |
|---|---|
|/managers/clearAlerts/Action|Schakel alle Hallo waarschuwingen die zijn gekoppeld aan Hallo Apparaatbeheer.|
|/managers/getActivationKey/Action|Activeringssleutel voor voor Apparaatbeheer Hallo ophalen.|
|/managers/regenerateActivationKey/Action|Activeringssleutel opnieuw genereren voor Apparaatbeheer Hallo.|
|/managers/regenarateRegistationCertificate/Action|Registratiecertificaat opnieuw genereren voor Hallo-apparaatbeheerprogramma.|
|/managers/getEncryptionKey/Action|Coderingssleutel voor Apparaatbeheer Hallo ophalen.|
|/managers/Read|Geeft een lijst of Managers voor apparaatregistratie Hallo opgehaald|
|/managers/DELETE|Hiermee verwijdert u Hallo Device Managers|
|managers/schrijven|Maken of bijwerken van Managers voor apparaatregistratie Hallo|
|/managers/configureDevice/Action|Hiermee configureert u een apparaat|
|/managers/listActivationKey/Action|Hallo activeringscode Hallo Apparaatbeheer StorSimple opgehaald.|
|/managers/listPublicEncryptionKey/Action|Lijst met codering met openbare sleutels van een StorSimple-Apparaatbeheer.|
|/managers/listPrivateEncryptionKey/Action|Persoonlijke sleutel voor een StorSimple-Apparaatbeheer opgehaald.|
|/managers/provisionCloudAppliance/Action|Maak een nieuw toestel in de cloud.|
|Managers/schrijftijd|Met de bewerking Kluis maken wordt een Azure-resource van het type vault gemaakt.|
|Managers/leestijd|Hallo kluis ophalen-bewerking een object dat Azure-resource van het type 'kluis' hello opgehaald|
|/ Managers/verwijderen|Hallo kluis verwijderen bewerking verwijderingen Hallo opgegeven Azure-resource van het type 'kluis'|
|/managers/storageAccountCredentials/Write|Maken of bijwerken van de Opslagaccountreferenties Hallo|
|/managers/storageAccountCredentials/Read|Geeft een lijst of Hallo Opslagaccountreferenties opgehaald|
|/managers/storageAccountCredentials/DELETE|Hiermee verwijdert u de Opslagaccountreferenties Hallo|
|/managers/storageAccountCredentials/listAccessKey/Action|Toegangstoetsen lijst van Opslagaccountreferenties|
|/managers/accessControlRecords/Read|Geeft een lijst of Hallo Access Control Records opgehaald|
|/managers/accessControlRecords/Write|Hallo Access Control Records maken of bijwerken|
|/managers/accessControlRecords/DELETE|Hallo Access Control Records worden verwijderd|
|/managers/metrics/Read|Geeft een lijst of Hallo metrische gegevens opgehaald|
|/managers/bandwidthSettings/Read|Hallo bandbreedte-instellingen weergeven (alleen 8000-serie)|
|/managers/bandwidthSettings/Write|Een nieuwe maken of bijwerken van de bandbreedte-instellingen (alleen 8000-serie)|
|/managers/bandwidthSettings/DELETE|Hiermee verwijdert u een bestaande bandbreedte-instellingen (alleen 8000-serie)|
|Managers/extendedInformation/leestijd|Hallo uitgebreide Info ophalen bewerking opgehaald van een object uitgebreid Info hello Azure-resource van het type dat vertegenwoordigt? kluis?|
|Managers/extendedInformation/schrijftijd|Hallo uitgebreide Info ophalen bewerking opgehaald van een object uitgebreid Info hello Azure-resource van het type dat vertegenwoordigt? kluis?|
|Managers, extendedInformation/verwijderen|Hallo uitgebreide Info ophalen bewerking opgehaald van een object uitgebreid Info hello Azure-resource van het type dat vertegenwoordigt? kluis?|
|/managers/Alerts/Read|Geeft een lijst of Hallo waarschuwingen opgehaald|
|/managers/storageDomains/Read|Geeft een lijst of Hallo opslag domeinen opgehaald|
|/managers/storageDomains/Write|Maken of bijwerken van Hallo opslag domeinen|
|/managers/storageDomains/DELETE|Hiermee verwijdert u Hallo opslag domeinen|
|/managers/Devices/scanForUpdates/Action|Zoeken naar updates in een apparaat.|
|/managers/Devices/Download/Action|Download updates voor een apparaat.|
|/managers/Devices/Install/Action|Updates installeren op een apparaat.|
|/managers/Devices/Read|Geeft een lijst of Hallo apparaten opgehaald|
|/managers/Devices/Write|Maken of bijwerken van Hallo-apparaten|
|/managers/Devices/DELETE|Hallo-apparaten worden verwijderd|
|/managers/Devices/Deactivate/Action|Een apparaat wordt gedeactiveerd.|
|/managers/Devices/publishSupportPackage/Action|Publiceer ondersteuningspakket van een apparaat voor het oplossen van Microsoft Support.|
|/managers/Devices/failover/Action|Failover van Hallo-apparaat.|
|/managers/Devices/sendTestAlertEmail/Action|Verzenden van e-mailwaarschuwingen van test tooconfigured e-mailontvangers.|
|/managers/Devices/installUpdates/Action|Updates worden geïnstalleerd op Hallo-apparaten|
|/managers/Devices/listFailoverSets/Action|Lijst Hallo failover wordt ingesteld voor een bestaand apparaat.|
|/managers/Devices/listFailoverTargets/Action|Doelen voor de failover van Hallo-apparaten|
|/managers/Devices/publicEncryptionKey/Action|Openbare versleutelingssleutel lijst van Hallo Apparaatbeheer|
|managers/apparaten/hardwareComponentGroups /<br>Lezen|Lijst Hallo Hardware onderdeelgroepen|
|managers/apparaten/hardwareComponentGroups /<br>changeControllerPowerState/actie|Controller voedingsstatus van hardware-onderdeelgroepen wijzigen|
|/managers/Devices/metrics/Read|Geeft een lijst of Hallo metrische gegevens opgehaald|
|/managers/Devices/chapSettings/Write|Hallo Chap-instellingen maken of bijwerken|
|/managers/Devices/chapSettings/Read|Geeft een lijst of ontvangt Hallo Chap-instellingen|
|/managers/Devices/chapSettings/DELETE|Hallo Chap-instellingen worden verwijderd|
|/managers/Devices/backupScheduleGroups/Read|Geeft een lijst of Hallo back-up schemagroepen opgehaald|
|/managers/Devices/backupScheduleGroups/Write|Hallo back-up schemagroepen maken of bijwerken|
|/managers/Devices/backupScheduleGroups/DELETE|Hallo back-up schemagroepen worden verwijderd|
|/managers/Devices/updateSummary/Read|Geeft een lijst of Hallo overzicht Update opgehaald|
|managers/apparaten/migrationSourceConfigurations /<br>actie/importeren|Importeren van de bron-configuraties voor migratie|
|managers/apparaten/migrationSourceConfigurations /<br>startMigrationEstimate/actie|Start een taak tooestimate Hallo duur van het migratieproces Hallo.|
|managers/apparaten/migrationSourceConfigurations /<br>startMigration/actie|Begint met de migratie met behulp van de bron-configuraties|
|managers/apparaten/migrationSourceConfigurations /<br>confirmMigration/actie|Bevestigt een succesvolle migratie en het doorvoeren.|
|managers/apparaten/migrationSourceConfigurations /<br>fetchMigrationEstimate/actie|Hallo-status voor de migratietaak schatting Hallo ophalen.|
|managers/apparaten/migrationSourceConfigurations /<br>fetchMigrationStatus/actie|Hallo-status voor de migratie Hallo ophalen.|
|managers/apparaten/migrationSourceConfigurations /<br>fetchConfirmMigrationStatus/actie|Hallo ophalen Bevestig de status van de migratie.|
|/managers/Devices/alertSettings/Read|Geeft een lijst of Hallo waarschuwingsinstellingen opgehaald|
|/managers/Devices/alertSettings/Write|Waarschuwing Hallo-instellingen maken of bijwerken|
|/managers/Devices/networkSettings/Read|Geeft een lijst of Hallo netwerkinstellingen opgehaald|
|/managers/Devices/networkSettings/Write|Een nieuwe maken of bijwerken van netwerkinstellingen|
|/managers/Devices/Jobs/Read|Geeft een lijst of Hallo taken opgehaald|
|/managers/Devices/Jobs/Cancel/Action|Een actieve taak annuleren|
|/managers/Devices/metricsDefinitions/Read|Geeft een lijst of Hallo metrische definities opgehaald|
|/managers/Devices/volumeContainers/Write|Maakt een nieuw of bijgewerkt Volumecontainers (alleen 8000-serie)|
|/managers/Devices/volumeContainers/Read|Hallo Volumecontainers lijst (alleen 8000-serie)|
|/managers/Devices/volumeContainers/DELETE|Hiermee verwijdert u een bestaande Volumecontainers (alleen 8000-serie)|
|/managers/Devices/volumeContainers/listEncryptionKeys/Action|De versleutelingssleutels lijst van Volumecontainers|
|/managers/Devices/volumeContainers/rolloverEncryptionKey/Action|De versleutelingssleutels rollover van Volumecontainers|
|/managers/Devices/volumeContainers/metrics/Read|Hallo metrische gegevens weergeven|
|/managers/Devices/volumeContainers/volumes/Read|Lijst Hallo Volumes|
|/managers/Devices/volumeContainers/volumes/Write|Een nieuwe maken of bijwerken van Volumes|
|/managers/Devices/volumeContainers/volumes/DELETE|Hiermee verwijdert u een bestaande Volumes|
|/managers/Devices/volumeContainers/volumes/metrics/Read|Hallo metrische gegevens weergeven|
|/managers/Devices/volumeContainers/volumes/metricsDefinitions/Read|Hallo definities van de metrische gegevens weergeven|
|/managers/Devices/volumeContainers/metricsDefinitions/Read|Hallo definities van de metrische gegevens weergeven|
|/managers/Devices/iscsiservers/Read|Geeft een lijst of Hallo iSCSI Servers opgehaald|
|/managers/Devices/iscsiservers/Write|Maken of bijwerken van Hallo iSCSI-Servers|
|/managers/Devices/iscsiservers/DELETE|Hiermee verwijdert u Hallo iSCSI-Servers|
|/managers/Devices/iscsiservers/Backup/Action|Duren back-up van een iSCSI-server.|
|/managers/Devices/iscsiservers/metrics/Read|Geeft een lijst of Hallo metrische gegevens opgehaald|
|/managers/Devices/iscsiservers/Disks/Read|Geeft een lijst of Hallo schijven opgehaald|
|/managers/Devices/iscsiservers/Disks/Write|Maken of bijwerken van Hallo-schijven|
|/managers/Devices/iscsiservers/Disks/DELETE|Hallo-schijven worden verwijderd|
|/managers/Devices/iscsiservers/Disks/metrics/Read|Geeft een lijst of Hallo metrische gegevens opgehaald|
|/managers/Devices/iscsiservers/Disks/metricsDefinitions/Read|Geeft een lijst of Hallo metrische definities opgehaald|
|/managers/Devices/iscsiservers/metricsDefinitions/Read|Geeft een lijst of Hallo metrische definities opgehaald|
|/managers/Devices/backups/Read|Geeft een lijst of back-upset Hallo opgehaald|
|/managers/Devices/backups/DELETE|Hiermee verwijdert u Hallo back-upset|
|/managers/Devices/backups/Restore/Action|Herstel alle Hallo-volumes van een back-upset.|
|/managers/Devices/backups/Elements/Clone/Action|Klonen van een share of het volume met behulp van een back-element.|
|/managers/Devices/backupPolicies/Write|Maakt een nieuw of bijgewerkt beleid van de back-up (alleen 8000-serie)|
|/managers/Devices/backupPolicies/Read|Lijst Hallo beleidsregels van back-up (alleen 8000-serie)|
|/managers/Devices/backupPolicies/DELETE|Hiermee verwijdert u een beleid in een bestaande back-up (alleen 8000-serie)|
|/managers/Devices/backupPolicies/Backup/Action|Een handmatige back-toocreate op aanvraag back-up van alle Hallo volumes die worden beveiligd door het beleid voor Hallo duren.|
|/managers/Devices/backupPolicies/Schedules/Write|Maakt een nieuw of bijgewerkt schema 's|
|/managers/Devices/backupPolicies/Schedules/Read|Lijst Hallo planningen|
|/managers/Devices/backupPolicies/Schedules/DELETE|Hiermee verwijdert u een bestaande planningen|
|/managers/Devices/securitySettings/update/Action|Hallo beveiligingsinstellingen bijwerken.|
|/managers/Devices/securitySettings/Read|Lijst Hallo beveiligingsinstellingen|
|managers/apparaten/securitySettings /<br>syncRemoteManagementCertificate/actie|Hallo-certificaat voor extern beheer voor een apparaat worden gesynchroniseerd.|
|/managers/Devices/securitySettings/Write|Maakt een nieuw of bijgewerkt beveiligingsinstellingen|
|/managers/Devices/fileservers/Read|Geeft een lijst of bestandsservers Hallo opgehaald|
|/managers/Devices/fileservers/Write|Maken of bijwerken van Hallo bestandsservers|
|/managers/Devices/fileservers/DELETE|Hiermee verwijdert u Hallo bestandsservers|
|/managers/Devices/fileservers/Backup/Action|Duren back-up van een bestandsserver.|
|/managers/Devices/fileservers/metrics/Read|Geeft een lijst of Hallo metrische gegevens opgehaald|
|/managers/Devices/fileservers/shares/Write|Maken of bijwerken van Hallo Shares|
|/managers/Devices/fileservers/shares/Read|Geeft een lijst of Hallo Shares opgehaald|
|/managers/Devices/fileservers/shares/DELETE|Hallo Shares worden verwijderd|
|/managers/Devices/fileservers/shares/metrics/Read|Geeft een lijst of Hallo metrische gegevens opgehaald|
|/managers/Devices/fileservers/shares/metricsDefinitions/Read|Geeft een lijst of Hallo metrische definities opgehaald|
|/managers/Devices/fileservers/metricsDefinitions/Read|Geeft een lijst of Hallo metrische definities opgehaald|
|/managers/Devices/timeSettings/Read|Geeft een lijst of Hallo tijdinstellingen opgehaald|
|/managers/Devices/timeSettings/Write|Maakt een nieuw of bijgewerkt tijdinstellingen|
|Managers/certificaten/schrijftijd|Hallo bewerking Update Resource certificaat updates Hallo resource/kluis referenties van het certificaat.|
|/managers/cloudApplianceConfigurations/Read|Lijst van ondersteunde configuraties voor Cloud toestel Hallo|
|/managers/metricsDefinitions/Read|Geeft een lijst of Hallo metrische definities opgehaald|
|/managers/encryptionSettings/Read|Geeft een lijst of versleutelingsinstellingen Hallo opgehaald|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Bewerking | Beschrijving |
|---|---|
|/streamingjobs/start/Action|Stream Analytics-taak starten|
|/streamingjobs/Stop/Action|Stream Analytics-taak stoppen|
|/ streamingjobs/lezen|Stream Analytics-taak lezen|
|/ streamingjobs/schrijven|Schrijven van Stream Analytics-taak|
|/ streamingjobs/verwijderen|Verwijderen van de Stream Analytics-taak|
|/streamingjobs/providers/Microsoft.Insights/metricDefinitions/Read|Hallo beschikbare metrische gegevens voor streamingjobs opgehaald|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/Read|Lees de diagnostische instelling.|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/Write|Diagnostische instelling schrijven.|
|/streamingjobs/providers/Microsoft.Insights/logDefinitions/Read|Hallo beschikbare logboeken opgehaald voor streamingjobs|
|/streamingjobs/Transformations/Read|Transformatie lezen Stream Analytics-taak|
|/streamingjobs/Transformations/Write|Stream Analytics-taak transformatie schrijven|
|/streamingjobs/Transformations/DELETE|Stream Analytics-taak transformatie verwijderen|
|/streamingjobs/inputs/Read|Invoer lezen Stream Analytics-taak|
|/streamingjobs/inputs/Write|Stream Analytics-taak invoer schrijven|
|/streamingjobs/inputs/DELETE|Stream Analytics-taak invoer verwijderen|
|/streamingjobs/outputs/Read|Lees Stream Analytics-Taakuitvoer|
|/streamingjobs/outputs/Write|Stream Analytics-Taakuitvoer schrijven|
|/streamingjobs/outputs/DELETE|Stream Analytics-Taakuitvoer verwijderen|

## <a name="microsoftsupport"></a>Microsoft.Support

| Bewerking | Beschrijving |
|---|---|
|registratie-/ actie|Registreert de tooSupport Resource Provider|
|/supportTickets/Read|Ondersteuningsticket details (inclusief status, ernst, contactgegevens en communicatie) opgehaald of Hallo lijst met Ondersteuningstickets voor abonnementen opgehaald.|
|supportTickets/schrijven|Maken of bijwerken van een Ondersteuningsticket. U kunt een Ondersteuningsticket maken voor technische, facturerings, quota's of beheer van abonnementen problemen met betrekking tot. U kunt de ernst, contactgegevens en communicatie voor bestaande ondersteuningstickets bijwerken.|

## <a name="microsoftweb"></a>Microsoft.Web

| Bewerking | Beschrijving |
|---|---|
|/ unregister/actie|Hef de registratie resourceprovider Microsoft.Web voor Hallo-abonnement.|
|valideren/actie|Valideren.|
|registratie-/ actie|De registerbronprovider Microsoft.Web voor Hallo-abonnement.|
|/ hostingEnvironments/lezen|Hallo-eigenschappen van een App-serviceomgeving opgehaald|
|/ hostingEnvironments/schrijven|Een nieuwe App Service-omgeving maken of bijwerken van bestaande|
|/ hostingEnvironments/verwijderen|Een App-serviceomgeving verwijderen|
|/hostingEnvironments/reboot/Action|Start opnieuw op alle machines in een App-serviceomgeving|
|/hostingenvironments/Resume/Action|Hervat de hostomgevingen.|
|/hostingenvironments/Suspend/Action|Onderbreken hostomgevingen.|
|/hostingenvironments/metricdefinitions/Read|Hosting-omgevingen metrische definities ophalen.|
|/hostingEnvironments/workerPools/Read|Hallo-eigenschappen van een werknemersgroep in een App-serviceomgeving opgehaald|
|/hostingEnvironments/workerPools/Write|Een nieuwe Worker-groep in een App Service-omgeving maken of bijwerken van een bestaande|
|/hostingenvironments/workerpools/metricdefinitions/Read|Hosting-omgevingen Workerpools metriek definities ophalen.|
|/hostingenvironments/workerpools/metrics/Read|Hosting-omgevingen Workerpools metrische gegevens ophalen.|
|/hostingenvironments/workerpools/skus/Read|Hosting-omgevingen Workerpools SKU's ophalen.|
|/hostingenvironments/workerpools/usages/Read|Hosting-omgevingen Workerpools gebruik ophalen.|
|/hostingenvironments/sites/Read|Hosting-omgevingen Web-Apps worden opgehaald.|
|/hostingenvironments/serverfarms/Read|Hosting-omgevingen App Service-abonnementen worden opgehaald.|
|/hostingenvironments/usages/Read|Hosting-omgevingen gebruik ophalen.|
|/hostingenvironments/capacities/Read|Hosting-omgevingen capaciteiten ophalen.|
|/hostingenvironments/Operations/Read|Hosting-omgevingen bewerkingen ophalen.|
|/hostingEnvironments/multiRolePools/Read|Hallo-eigenschappen van een FrontEnd-toepassingen in een App-serviceomgeving opgehaald|
|/hostingEnvironments/multiRolePools/Write|Een nieuwe FrontEnd-toepassingen in een App Service-omgeving maken of bijwerken van een bestaande|
|/hostingenvironments/multirolepools/metricdefinitions/Read|Hosting-omgevingen MultiRole Pools metrische definities ophalen.|
|/hostingenvironments/multirolepools/metrics/Read|Hosting-omgevingen MultiRole Pools metrische gegevens ophalen.|
|/hostingenvironments/multirolepools/skus/Read|Hosting-omgevingen MultiRole Pools SKU's ophalen.|
|/hostingenvironments/multirolepools/usages/Read|Hosting-omgevingen MultiRole Pools gebruik ophalen.|
|/hostingenvironments/Diagnostics/Read|Hosting-omgevingen diagnostische gegevens ophalen.|
|/publishingusers/Read|Publiceren van gebruikers ophalen.|
|publishingusers/schrijven|Bijwerken van de gebruikers te publiceren.|
|/checknameavailability/Read|Controleer of de resourcenaam van de beschikbaar is.|
|/ geoRegions/lezen|Hallo-lijst met Geo regions ophalen.|
|/ sites/lezen|Hallo-eigenschappen van een Web-App opgehaald|
|/ sites/schrijven|Een nieuwe Web-App maken of bijwerken van een bestaande|
|/ sites/verwijderen|Een bestaande Web-App verwijderen|
|/sites/Backup/Action|Een nieuwe web-app back-up maken|
|/sites/PublishXml/Action|Ophalen van de xml van profiel voor een Web-App publiceren|
|/sites/Publish/Action|Een Web-App publiceren|
|/sites/restart/Action|Een Web-App starten|
|/sites/start/Action|Een Web-App starten|
|/sites/Stop/Action|Een Web-App stoppen|
|/sites/slotsswap/Action|Implementatie Web-appsites wisselen|
|/sites/slotsdiffs/Action|Verschillen in de configuratie tussen web-app en sleuven ophalen|
|/sites/applySlotConfig/Action|Web-app-siteconfiguratie van doel sleuf toohello huidige web-app toepassen|
|/sites/resetSlotConfig/Action|Web-app-configuratie opnieuw instellen|
|/sites/Functions/Action|Functies van Web-Apps.|
|/sites/listsyncfunctiontriggerstatus/Action|Lijst met synchronisatie functie Trigger Status Web-Apps.|
|/sites/networktrace/Action|Netwerk Trace Web-Apps.|
|/sites/NewPassword/Action|NieuwWachtwoord Web-Apps.|
|/sites/Sync/Action|Synchronisatie van Web-Apps.|
|/sites/operationresults/Read|Web-Apps Bewerkingsresultaten krijgt.|
|/sites/webjobs/Read|Web-Apps webtaken worden opgehaald.|
|/ sites/back-up/lezen|Back-up van Web Apps ophalen.|
|/sites/Backup/Write|Back-up van Web-Apps worden bijgewerkt.|
|/sites/metricdefinitions/Read|Web-Apps metriek definities worden opgehaald.|
|/sites/metrics/Read|Web-Apps metrische gegevens worden opgehaald.|
|/sites/continuouswebjobs/DELETE|Web-Apps doorlopende webtaken verwijderen.|
|/sites/continuouswebjobs/Read|Web-Apps doorlopende webtaken worden opgehaald.|
|/sites/continuouswebjobs/start/Action|Web-Apps doorlopende webtaken starten.|
|/sites/continuouswebjobs/Stop/Action|Web-Apps doorlopende webtaken stoppen.|
|/sites/domainownershipidentifiers/Read|Web-Apps domein eigenaar-id's worden opgehaald.|
|/sites/domainownershipidentifiers/Write|Web-Apps domein eigenaar-id's worden bijgewerkt.|
|/sites/premieraddons/DELETE|Web Apps Premier invoegtoepassingen verwijderen.|
|/sites/premieraddons/Read|Web Apps Premier invoegtoepassingen ophalen.|
|/sites/premieraddons/Write|Bijwerken van Web Apps Premier invoegtoepassingen.|
|/sites/triggeredwebjobs/DELETE|Web-Apps Triggered webtaken verwijderen.|
|/sites/triggeredwebjobs/Read|Web-Apps Triggered webtaken worden opgehaald.|
|/sites/triggeredwebjobs/Run/Action|Geactiveerde WebJobs voor Web-Apps worden uitgevoerd.|
|/sites/hostnamebindings/DELETE|Hostnaambindings voor Web-Apps verwijderen.|
|/sites/hostnamebindings/Read|Web-Apps Hostnaambindings ophalen.|
|/sites/hostnamebindings/Write|Web-Apps Hostnaambindings bijwerken.|
|/sites/virtualnetworkconnections/DELETE|Verwijder virtuele netwerkverbindingen van Web Apps.|
|/sites/virtualnetworkconnections/Read|Web-Apps virtuele netwerkverbindingen worden opgehaald.|
|/sites/virtualnetworkconnections/Write|Web-Apps virtuele netwerkverbindingen worden bijgewerkt.|
|/sites/virtualnetworkconnections/gateways/Read|Web-Apps virtuele verbindingen netwerkgateways ophalen.|
|/sites/virtualnetworkconnections/gateways/Write|Web-Apps virtueel netwerk verbindingen Gateways bijwerken.|
|/sites/PublishXml/Read|Web-Apps publiceren XML ophalen.|
|/sites/hybridconnectionrelays/Read|Web-Apps hybride verbinding Relays ophalen.|
|/sites/perfcounters/Read|Prestatiemeteritems voor Web-Apps worden opgehaald.|
|/sites/usages/Read|Het gebruik van Web Apps ophalen.|
|/sites/slots/Write|Een nieuwe Web-Appsite maken of bijwerken van een bestaande|
|/sites/slots/DELETE|Een bestaande Web-Appsite verwijderen|
|/sites/slots/Backup/Action|Nieuwe Web-Appsite back-up maken.|
|/sites/slots/PublishXml/Action|Profiel xml publiceren voor Web-Appsite ophalen|
|/sites/slots/Publish/Action|Een Web-Appsite publiceren|
|/sites/slots/restart/Action|Een Web-Appsite starten|
|/sites/slots/start/Action|Een Web-Appsite starten|
|/sites/slots/Stop/Action|Een Web-Appsite stoppen|
|/sites/slots/slotsswap/Action|Implementatie Web-appsites wisselen|
|/sites/slots/slotsdiffs/Action|Verschillen in de configuratie tussen web-app en sleuven ophalen|
|/sites/slots/applySlotConfig/Action|Web-app-siteconfiguratie van doel sleuf toohello huidige sleuf toepassen.|
|/sites/slots/resetSlotConfig/Action|Web-app sleuf configuratie opnieuw instellen|
|/sites/slots/Read|Hallo-eigenschappen van een Web-App implementatiesleuf opgehaald|
|/sites/slots/NewPassword/Action|Sleuven NieuwWachtwoord Web-Apps.|
|/sites/slots/Sync/Action|Synchronisatie Web Apps sleuven.|
|/sites/slots/operationresults/Read|Web-Apps sleuven Bewerkingsresultaten krijgt.|
|/sites/slots/webjobs/Read|Web-Apps sleuven webtaken worden opgehaald.|
|/sites/slots/Backup/Write|Bijwerken van Web Apps sleuven back-up.|
|/sites/slots/metricdefinitions/Read|Web-Apps sleuven metrische definities worden opgehaald.|
|/sites/slots/metrics/Read|Web-Apps sleuven metrische gegevens worden opgehaald.|
|/sites/slots/continuouswebjobs/DELETE|Web-Apps sleuven doorlopende webtaken verwijderen.|
|/sites/slots/continuouswebjobs/Read|Web-Apps sleuven doorlopende webtaken worden opgehaald.|
|/sites/slots/continuouswebjobs/start/Action|Web-Apps sleuven doorlopende webtaken starten.|
|/sites/slots/continuouswebjobs/Stop/Action|Web-Apps sleuven doorlopende webtaken stoppen.|
|/sites/slots/premieraddons/DELETE|Web Apps sleuven Premier invoegtoepassingen verwijderen.|
|/sites/slots/premieraddons/Read|Web Apps sleuven Premier invoegtoepassingen ophalen.|
|/sites/slots/premieraddons/Write|Bijwerken van Web Apps sleuven Premier invoegtoepassingen.|
|/sites/slots/triggeredwebjobs/DELETE|Web-Apps sleuven Triggered webtaken verwijderen.|
|/sites/slots/triggeredwebjobs/Read|Web-Apps sleuven Triggered webtaken worden opgehaald.|
|/sites/slots/triggeredwebjobs/Run/Action|Web-Apps sleuven Triggered webtaken worden uitgevoerd.|
|/sites/slots/hostnamebindings/DELETE|Web-Apps sleuven Hostnaambindings verwijderen.|
|/sites/slots/hostnamebindings/Read|Web-Apps sleuven Hostnaambindings ophalen.|
|/sites/slots/hostnamebindings/Write|Web-Apps sleuven Hostnaambindings bijwerken.|
|/sites/slots/phplogging/Read|Web-Apps sleuven Phplogging ophalen.|
|/sites/slots/virtualnetworkconnections/DELETE|Web-Apps sleuven virtuele netwerkverbindingen verwijderen.|
|/sites/slots/virtualnetworkconnections/Read|Web-Apps sleuven virtuele netwerkverbindingen worden opgehaald.|
|/sites/slots/virtualnetworkconnections/Write|Web-Apps sleuven virtuele netwerkverbindingen worden bijgewerkt.|
|/sites/slots/virtualnetworkconnections/gateways/Write|Web-Apps sleuven virtueel netwerk verbindingen Gateways bijwerken.|
|/sites/slots/usages/Read|Het gebruik van Web Apps sleuven ophalen.|
|/sites/slots/hybridconnection/DELETE|Sleuven hybride verbinding voor Web-Apps verwijderen.|
|/sites/slots/hybridconnection/Read|Hybride verbinding voor Web-Apps sleuven ophalen.|
|/sites/slots/hybridconnection/Write|Hybride verbinding voor Web-Apps sleuven bijwerken.|
|/sites/slots/config/Read|Web-Appsite van configuratie-instellingen ophalen|
|/sites/slots/config/List/Action|Web-Appsite van gevoelige beveiligingsinstellingen, zoals het publiceren van referenties, app-instellingen en verbindingsreeksen weergeven|
|/sites/slots/config/Write|Web-Appsite van configuratie-instellingen bijwerken|
|/sites/slots/config/DELETE|Webconfiguratie Apps sleuven verwijderen.|
|/sites/slots/Instances/Read|Web-Apps sleuven instanties worden opgehaald.|
|/sites/slots/Instances/processes/Read|Web-Apps sleuven exemplaren processen worden opgehaald.|
|/sites/slots/Instances/Deployments/Read|Implementaties van Web Apps sleuven instanties worden opgehaald.|
|/sites/slots/sourcecontrols/Read|Configuratie-instellingen voor Web-Appsite van broncodebeheer ophalen|
|/sites/slots/sourcecontrols/Write|Instellingen voor Web-Appsite van bronbeheer configuratie bijwerken|
|/sites/slots/sourcecontrols/DELETE|Instellingen voor Web-Appsite van bronbeheer configuratie verwijderen|
|/sites/slots/Restore/Read|Web-Apps sleuven terugzetten ophalen.|
|/sites/slots/analyzecustomhostname/Read|Ophalen van Web Apps sleuven analyseren aangepaste hostnaam.|
|/sites/slots/backups/Read|Eigenschappen van back-up van een web-appsites hello opgehaald|
|/sites/slots/backups/List/Action|Lijst met Web-Apps sleuven back-ups.|
|/sites/slots/backups/Restore/Action|Web-Apps sleuven back-ups herstellen.|
|/sites/slots/Deployments/DELETE|Web-Apps sleuven implementaties verwijderd.|
|/sites/slots/Deployments/Read|Web-Apps sleuven implementaties ophalen.|
|/sites/slots/Deployments/Write|Update-implementaties van Web Apps sleuven.|
|/sites/slots/Deployments/log/Read|Web-Apps sleuven implementaties logboek ophalen.|
|/sites/hybridconnection/DELETE|Web-Apps hybride verbinding verwijderen.|
|/sites/hybridconnection/Read|Verbinding voor Web-Apps hybride ophalen.|
|/sites/hybridconnection/Write|Web-Apps hybride verbinding bijwerken.|
|/sites/recommendationhistory/Read|Web-Apps aanbeveling geschiedenis ophalen.|
|/sites/Recommendations/Read|Lijst met aanbevelingen voor web-app Hallo ophalen.|
|/sites/Recommendations/Disable/Action|Web-Apps aanbevelingen uitschakelen.|
|/sites/config/Read|Ophalen van configuratie-instellingen voor Web-App|
|/sites/config/List/Action|Web-App gevoelige beveiligingsinstellingen, zoals het publiceren van referenties, app-instellingen en verbindingsreeksen weergeven|
|/sites/config/Write|Configuratie-instellingen voor Web-App bijwerken|
|/sites/config/DELETE|Webconfiguratie Apps verwijderen.|
|/sites/Instances/Read|Web-Apps instanties worden opgehaald.|
|/sites/Instances/processes/DELETE|Web-Apps exemplaren processen verwijderen.|
|/sites/Instances/processes/Read|Web-Apps exemplaren processen worden opgehaald.|
|/sites/Instances/Deployments/Read|Implementaties van Web Apps instanties worden opgehaald.|
|/sites/sourcecontrols/Read|Broncodebeheer voor Web-App-configuratie-instellingen ophalen|
|/sites/sourcecontrols/Write|Instellingen voor Web-App bronbeheer configuratie bijwerken|
|/sites/sourcecontrols/DELETE|Instellingen voor Web-App bronbeheer configuratie verwijderen|
|/sites/Restore/Read|Terugzetten van de Web-Apps worden opgehaald.|
|/sites/analyzecustomhostname/Read|Analyseer de aangepaste hostnaam.|
|/sites/backups/Read|Hallo-eigenschappen van een web-app back-up opgehaald|
|/sites/backups/List/Action|Lijst met Web-Apps back-ups.|
|/sites/backups/Restore/Action|Terugzetten van back-ups van Web-Apps.|
|/sites/Snapshots/Read|Momentopnamen van de Web-Apps ophalen.|
|/sites/Functions/DELETE|Functies voor Web-Apps verwijderen.|
|/sites/Functions/listsecrets/Action|Lijst met geheimen Web Apps functies.|
|/sites/Functions/Read|Functies voor Web-Apps worden opgehaald.|
|/sites/Functions/Write|Bijwerken van Web Apps functies.|
|/sites/Deployments/DELETE|Implementaties van Web-Apps verwijderd.|
|/sites/Deployments/Read|Implementaties van Web-Apps worden opgehaald.|
|/sites/Deployments/Write|Update-implementaties van Web-Apps.|
|/sites/Deployments/log/Read|Web-Apps implementaties logboek ophalen.|
|/sites/Diagnostics/Read|Web-Apps diagnostische gegevens worden opgehaald.|
|/sites/Diagnostics/workerprocessrecycle/Read|Recyclen van Web Apps Diagnostics Worker proces worden opgehaald.|
|/sites/Diagnostics/workeravailability/Read|Web-Apps Diagnostics Workeravailability ophalen.|
|/sites/Diagnostics/runtimeavailability/Read|Runtime-beschikbaarheid van Web-Apps diagnostische gegevens worden opgehaald.|
|/sites/Diagnostics/cpuanalysis/Read|Web-Apps Diagnostics Cpuanalysis ophalen.|
|/sites/Diagnostics/servicehealth/Read|Servicestatus van Web Apps diagnostische gegevens worden opgehaald.|
|/sites/Diagnostics/frebanalysis/Read|Web-Apps Diagnostics FREB analyse worden opgehaald.|
|/availablestacks/Read|Beschikbare Stacks ophalen.|
|/isusernameavailable/Read|Controleer of de gebruikersnaam beschikbaar is.|
|/Microsoft.Web/apiManagementAccounts/<br>API's leestijd|Hallo lijst ophalen van API's.|
|/Microsoft.Web/apiManagementAccounts/<br>API's / schrijven|Een nieuwe Api toevoegen of bijwerken van bestaande.|
|/Microsoft.Web/apiManagementAccounts/<br>API's en verwijderen|Verwijder een bestaande Api.|
|/Microsoft.Web/apiManagementAccounts/<br>verbindingen API's leestijd|Hallo-lijst met verbindingen opgehaald.|
|/Microsoft.Web/apiManagementAccounts/<br>verbindingen API's schrijftijd|Sla een nieuwe verbinding of een bestaande bijgewerkt.|
|/Microsoft.Web/apiManagementAccounts/<br>API's, verbindingen, verwijderen|Verwijder een bestaande verbinding.|
|/Microsoft.Web/apiManagementAccounts/<br>API's verbindingen/connectionAcls/leestijd|ConnectionAcls lezen|
|/Microsoft.Web/apiManagementAccounts/<br>API's / verbindingen/connectionAcls/schrijven|Toevoegen of bijwerken van ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>API's, verbindingen, connectionAcls/verwijderen|ConnectionAcl verwijderen|
|/Microsoft.Web/apiManagementAccounts/<br>connectionAcls API's leestijd|Lees ConnectionAcls voor Api|
|/Microsoft.Web/apiManagementAccounts/<br>apiAcls API's leestijd|ConnectionAcls lezen|
|/Microsoft.Web/apiManagementAccounts/<br>apiAcls API's schrijftijd|Maken of bijwerken van de Api-ACL 's|
|/Microsoft.Web/apiManagementAccounts/<br>API's, apiAcls, verwijderen|Api-ACL's verwijderen|
|/ serverfarms/lezen|Hallo-eigenschappen ophalen op een App Service-Plan|
|/ serverfarms/schrijven|Maak een nieuwe App Service-abonnement of een bestaande bijgewerkt|
|/ serverfarms/verwijderen|Verwijder een bestaande App Service-Plan|
|/serverfarms/restartSites/Action|Start opnieuw op alle Web-Apps in een App Service-Plan|
|/serverfarms/operationresults/Read|App Service-abonnementen Bewerkingsresultaten krijgt.|
|/serverfarms/Capabilities/Read|Mogelijkheden van App Service-abonnementen ophalen.|
|/serverfarms/metricdefinitions/Read|App Service-abonnementen metrische definities worden opgehaald.|
|/serverfarms/metrics/Read|App Service-abonnementen metrische gegevens worden opgehaald.|
|/serverfarms/hybridconnectionplanlimits/Read|Ophalen van App Service-abonnementen hybride verbindingslimieten-Plan.|
|/serverfarms/virtualnetworkconnections/Read|App Service-abonnementen virtuele netwerkverbindingen worden opgehaald.|
|/serverfarms/virtualnetworkconnections/routes/DELETE|App Service-abonnementen virtueel netwerk verbindingen Routes verwijderen.|
|/serverfarms/virtualnetworkconnections/routes/Read|App Service-abonnementen virtueel netwerk verbindingen Routes worden opgehaald.|
|/serverfarms/virtualnetworkconnections/routes/Write|App Service-abonnementen virtueel netwerk verbindingen Routes bijwerken.|
|/serverfarms/virtualnetworkconnections/gateways/Write|App Service-abonnementen virtueel netwerk verbindingen Gateways bijwerken.|
|/serverfarms/firstpartyapps/Settings/DELETE|App Service-abonnementen eerste partijen Apps instellingen verwijderd.|
|/serverfarms/firstpartyapps/Settings/Read|App Service-abonnementen eerste partijen Apps-instellingen ophalen.|
|/serverfarms/firstpartyapps/Settings/Write|App Service-abonnementen eerste partijen Apps instellingen worden bijgewerkt.|
|/serverfarms/sites/Read|Web-Apps van App Service-abonnementen ophalen.|
|/serverfarms/workers/reboot/Action|Start opnieuw op App Service-abonnementen werknemers.|
|/serverfarms/hybridconnectionrelays/Read|App Service-abonnementen hybride verbinding Relays ophalen.|
|/serverfarms/skus/Read|App Service-abonnementen SKU's worden opgehaald.|
|/serverfarms/usages/Read|Het gebruik van App Service-abonnementen ophalen.|
|/serverfarms/hybridconnectionnamespaces/relays/sites/Read|App Service-plannen voor hybride verbinding naamruimten Relays WebApps ophalen.|
|/ishostnameavailable/Read|Controleer of de hostnaam beschikbaar is.|
|/ connectionGateways/lezen|Hallo-lijst van Gateways verbinding ophalen.|
|/ connectionGateways/schrijven|Maken of bijwerken van een Gateway-verbinding.|
|/ connectionGateways/verwijderen|Hiermee verwijdert u een Gateway verbinding.|
|/connectionGateways/join/Action|Een Gateway verbinding koppelt.|
|/classicmobileservices/Read|Klassieke mobiele Services krijgen.|
|/skus/Read|SKU's worden opgehaald.|
|certificaten/lezen|Hallo-lijst van certificaten ophalen.|
|certificaten/schrijven|Voeg een nieuw certificaat of een bestaande bijgewerkt.|
|certificaten/verwijderen|Een bestaand certificaat verwijderen.|
|/Operations/Read|Bewerkingen ophalen.|
|/ aanbevelingen/lezen|Hallo-lijst met aanbevelingen voor abonnementen ophalen.|
|/ishostingenvironmentnameavailable/Read|Get als de naam van de Hosting-omgeving beschikbaar is.|
|/ apiManagementAccounts/lezen|Hallo-lijst met ApiManagementAccounts ophalen.|
|/ apiManagementAccounts/schrijven|Een nieuwe ApiManagementAccount toevoegen of een bestaande bijgewerkt|
|/ apiManagementAccounts/verwijderen|Een bestaande ApiManagementAccount verwijderen|
|/apiManagementAccounts/connectionAcls/Read|Hallo-lijst met ACL's verbinding ophalen.|
|/apiManagementAccounts/apiAcls/Read|ConnectionAcls lezen|
|/ verbindingen/lezen|Hallo-lijst met verbindingen opgehaald.|
|/ verbindingen/schrijven|Maken of bijwerken van een verbinding.|
|/ verbindingen/verwijderen|Hiermee verwijdert u een verbinding.|
|/Connections/join/Action|Lid van een verbinding.|
|/Connections/confirmconsentcode/Action|Controleer de verbindingen toestemming Code.|
|/Connections/listconsentlinks/Action|Lijst met toestemming koppelingen voor verbindingen.|
|/deploymentlocations/Read|Implementatie locaties ophalen.|
|/sourcecontrols/Read|Besturingselementen voor gegevensbronnen worden opgehaald.|
|sourcecontrols/schrijven|Besturingselementen voor gegevensbronnen bijwerken.|
|/managedhostingenvironments/Read|Ophalen van beheerde hostomgevingen.|
|/managedhostingenvironments/sites/Read|Ophalen van beheerde die als host fungeert voor de Web-Apps omgevingen.|
|/managedhostingenvironments/serverfarms/Read|Ophalen van beheerde omgevingen App Service-abonnementen die als host fungeert.|
|/Locations/managedapis/Read|Locaties beheerde API's worden opgehaald.|
|/Locations/apioperations/Read|Locaties API-bewerkingen ophalen.|
|/Locations/connectiongatewayinstallations/Read|Locaties verbinding Gateway installaties worden opgehaald.|
|/ listSitesAssignedToHostName/lezen|Namen van sites die zijn toegewezen toohostname ophalen.|

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe te[maakt u een aangepaste rol](role-based-access-control-custom-roles.md).

- Bekijk Hallo [ingebouwde RBAC-rollen](role-based-access-built-in-roles.md).

- Meer informatie over hoe toomanage toegang tot toewijzingen [door gebruiker](role-based-access-control-manage-assignments.md) of [door resource](role-based-access-control-configure.md) 
