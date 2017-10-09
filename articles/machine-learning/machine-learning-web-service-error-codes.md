---
title: foutcodes voor aaaAzure Machine Learning REST API | Microsoft Docs
description: Deze foutcodes kunnen worden geretourneerd door een bewerking op een Azure Machine Learning-webservice.
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Machine Learning-REST API-foutcodes
 
Hallo kunnen volgende foutcodes worden geretourneerd door een bewerking op een Azure Machine Learning-webservice.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (HTTP-statuscode 400)
 
Ongeldig argument opgegeven.
 
Deze klasse van fouten betekent een ergens opgegeven argument is ongeldig. Dit kan een referentie of de locatie van Azure storage toosomething toohello webservice doorgegeven worden. Raadpleeg Hallo 'foutcode' veld in Hallo "gegevens" sectie toodiagnose welke specifieke argument ongeldig is.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| BadParameterValue | Hallo-parameterwaarde opgegeven voldoet niet aan Hallo parameter regel Hallo-parameter |
| BadSubscriptionId | Hallo abonnement-Id die is gebruikt tooscore is niet Hallo een aanwezig is in Hallo resource |
| BadVersionCall | Ongeldige versie-parameter is doorgegeven tijdens Hallo API-aanroep: {0}. Controleer Hallo API help-pagina voor het doorgeven van de juiste versie Hallo en probeer het opnieuw. |
| BatchJobInputsNotSpecified | Hallo na vereist input(s) zijn niet wordt opgegeven met de Hallo-aanvraag: {0}. Controleer of alle ingevoerde gegevens is opgegeven en probeer het opnieuw. |
| BatchJobInputsTooManySpecified | Hallo-aanvraag opgegeven meer invoerwaarden dan gedefinieerd in het Hallo-service. Lijst met geaccepteerde input(s): {0}. Controleer of alle ingevoerde gegevens correct is opgegeven en probeer het opnieuw. |
| BlobNameTooLong | Azure blob storage-pad opgegeven voor diagnostische uitvoer te lang is: {0}. Hallo pad kort en probeer het opnieuw. |
| BlobNotFound | Kan geen tooaccess Hallo opgegeven Azure blob - {0}.  Azure-foutbericht: {1}. |
| ContainerIsEmpty | Er is geen Azure-opslag-containernaam is opgegeven. Geef een geldige container op en probeer het opnieuw. |
| ContainerSegmentInvalid | De containernaam is ongeldig. Geef een geldige container op en probeer het opnieuw. |
| ContainerValidationFailed | BLOB-container-validatie is mislukt vanwege de volgende fout: {0}. |
| DataTypeNotSupported | Niet-ondersteund gegevenstype opgegeven. Geef geldige gegevenstypen en probeer het opnieuw. |
| DuplicateInputInBatchCall | Hallo batch-aanvraag is ongeldig. Kan niet zowel één als meerdere invoer op Hallo dezelfde opgeven tijd. Een van deze items verwijderen uit het Hallo-aanvraag en probeer het opnieuw. |
| ExpiryTimeInThePast | Verlooptijd opgegeven is in de afgelopen Hallo: {0}. Geef een toekomstige vervaldatum UTC-tijd en probeer het opnieuw. toonever verloopt, verlopen tijd tooNULL is ingesteld. |
| IncompleteSettings | Diagnostische instellingen zijn onvolledig. |
| InputBlobRelativeLocationInvalid | Er is geen Azure storage blob-naam opgegeven. Geef een geldige blob-naam en probeer het opnieuw. |
| InvalidBlob | Ongeldige blob-specificatie voor blob: {0}. Controleer of deze verbindingsreeks / relatief pad of SAS-token specificatie juist is en probeer het opnieuw. |
| InvalidBlobConnectionString | Hallo verbindingsreeks die is opgegeven voor een Hallo input/output blobs in een ongeldig: {0}. Corrigeer deze en probeer het opnieuw. |
| InvalidBlobExtension | Hallo blobverwijzing: {0} heeft een ongeldige of ontbrekende bestandsextensie. Bestandsextensies ondersteund voor dit uitvoertype zijn: '{1}'. |
| InvalidInputNames | Ongeldige service namen die zijn opgegeven in de aanvraag Hallo invoer: {0}. Hallo invoergegevens toohello juiste service invoer worden toegewezen en probeer het opnieuw. |
| InvalidOutputOverrideName | Ongeldige uitvoer naam overschrijven: {0}. Hallo-service beschikt niet over een knooppunt uitvoer met deze naam. Geef een juiste uitvoer knooppunt naam toooverride (hoofdlettergevoeligheid van toepassing). |
| InvalidQueryParameter | Ongeldige queryparameter {0}. {1} |
| MissingInputBlobInformation | Ontbrekende informatie voor Azure storage-blob. Geef een geldige verbindingsreeks en de relatief pad of de URI en probeer het opnieuw. |
| MissingJobId | Er is geen taak-Id opgegeven. Een taak Id wordt geretourneerd wanneer een taak is ingediend voor Hallo eerst. Controleer of Hallo taak-Id juist is en probeer het opnieuw. |
| MissingKeys | Er zijn geen sleutels opgegeven of een van de primaire of secundaire sleutel is niet opgegeven. |
| MissingModelPackage | Geen pakket-Id van model of model pakket die zijn opgegeven. Geef de pakket-Id van een geldig model of model pakket en probeer het opnieuw. |
| MissingOutputOverrideSpecification | Hallo-aanvraag ontbreekt Hallo blob-specificatie voor onderdrukking van de uitvoer {0}. Geef een geldige blob-locatie met Hallo aanvraag, of verwijder Hallo uitvoerspecificatie geen overschrijving locatie desgewenst. |
| MissingRequestInput | Hallo-webservice invoer verwacht, maar er is niets is opgegeven. Ervoor geldige invoer worden geleverd op basis van Hallo gepubliceerd poorten in Hallo model invoer en probeer het opnieuw. |
| MissingRequiredGlobalParameters | Niet alle vereiste web service parameters opgegeven. Controleer of Hallo parameter (s) verwacht voor Hallo modules juist zijn en probeer het opnieuw. |
| MissingRequiredOutputOverrides | Bij het aanroepen van een versleutelde service-eindpunt is verplicht toopass in onderdrukt de uitvoer voor de uitvoer van alle Hallo-service. Onderdrukkingen op dit moment voor deze uitvoer ontbreekt: {0} |
| MissingWebServiceGroupId | Er is geen groep web service-Id opgegeven. Geef een geldige webservice-servicegroep Id en probeer het opnieuw. |
| MissingWebServiceId | Geen webservice-Id opgegeven. Geef een geldige webservice Id en probeer het opnieuw. |
| MissingWebServicePackage | Er is geen web Service-pakket opgegeven. Geef een geldige web service-pakket op en probeer het opnieuw. |
| MissingWorkspaceId | Er is geen werkruimte-Id opgegeven. Geef een geldige Id-werkruimte en probeer het opnieuw. |
| ModelConfigurationInvalid | Ongeldig modeltype configuratie in Hallo model pakket. Zorg ervoor dat Hallo Modelconfiguratie bevat een definitie in de uitvoer-eindpunten, std fout eindpunt, en std eindpunt af en probeer het opnieuw. |
| ModelPackageIdInvalid | Ongeldig modeltype pakket-id. Verifieer dat Hallo model pakket-Id juist is en probeer het opnieuw. |
| RequestBodyInvalid | Er is geen aanvraagtekst opgegeven of fout bij het deserialiseren van de aanvraagtekst Hallo. |
| RequestIsEmpty | Er is geen aanvraag opgenomen. Geef een geldige aanvraag en probeer het opnieuw. |
| UnexpectedParameter | Onverwachte parameters die worden geleverd. Controleer of alle parameternamen correct zijn gespeld, alleen verwachte parameters worden doorgegeven en probeer het opnieuw. |
| UnknownError | Onbekende fout opgetreden. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | Kan de vereisten voor gelijktijdige aanvragen voor de webservice {0} niet wijzigen. |
| WebServiceIdInvalid | Ongeldige webservice-id opgegeven. Webservice-id moet een geldige guid zijn. |
| WebServiceTooManyConcurrentRequestRequirement | Gelijktijdige aanvraag vereiste toomore dan {0} kan niet worden ingesteld. |
| WebServiceTypeInvalid | Ongeldige web service type dat is opgegeven. Controleer of Hallo geldig web servicetype juist is en probeer het opnieuw. Geldige webservice servicetypen: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (HTTP-statuscode 400)
 
Ongeldige gebruiker groepsargument opgegeven.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| InputMismatchError | Invoergegevens komt niet overeen voor invoerpoort schema. |
| InputParseError | Het parseren van de invoer-vector is mislukt.  Controleer of Hallo invoer vector heeft Hallo juiste aantal kolommen en gegevenstypen.  Aanvullende informatie: {0}. |
| MissingRequiredGlobalParameters | Parameter (s) werd verwacht door de webservice Hallo ontbreken. Controleer of alle vereiste Hallo parameters verwacht door de webservice Hallo juist zijn en probeer het opnieuw. |
| UnexpectedParameter | Controleer of alleen Hallo vereiste parameters verwacht door de webservice Hallo worden doorgegeven en probeer het opnieuw. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (HTTP-statuscode 400)
 
Hallo-aanvraag is ongeldig in de huidige context Hallo.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| CannotStartJob | Hallo-taak kan niet worden gestart omdat het {0} status heeft. |
| IncompatibleModel | Hallo-model is incompatibel met de versie van de aanvraag Hallo. Hallo aanvraag versie ondersteunt alleen één datatable uitvoer modellen. |
| MultipleInputsNotAllowed | Hallo model kunnen niet meerdere invoer. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (HTTP-statuscode 400)
 
Uitvoering van module is een interne bibliotheek opgetreden.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (HTTP-statuscode 400)
 
Uitvoering van module is een fout opgetreden.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (HTTP-statuscode 400)
 
Ongeldige web service-pakket. Controleer of Hallo web servicepakket opgegeven juist is en probeer het opnieuw.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| FormatError | Hallo web service-pakket is niet goed gevormd. Details: {0} |
| RuntimesError | Hallo web service pakket grafiek is ongeldig. Details: {0} |
| ValidationError | Hallo web service pakket grafiek is ongeldig. Details: {0} |
 
## <a name="unauthorized-http-status-code-401"></a>Niet-geautoriseerde (HTTP-statuscode 401)
 
Aanvraag is niet-geautoriseerde tooaccess resource.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| AdminRequestUnauthorized | Niet geautoriseerd |
| ManagementRequestUnauthorized | Niet geautoriseerd |
| ScoreRequestUnauthorized | Ongeldige referenties opgegeven. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (HTTP-statuscode 404)
 
Kan de resource niet vinden.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| ModelPackageNotFound | Model-pakket niet gevonden. Controleer of Hallo model pakket-Id juist is en probeer het opnieuw. |
| WebServiceIdNotFoundInWorkspace | Web-service onder deze werkruimte niet gevonden. Er is een Hallo webServiceId en Hallo workspaceId komen niet overeen. Controleer of Hallo webservice opgegeven maakt deel uit van de werkruimte Hallo en probeer het opnieuw. |
| WebServiceNotFound | De webservice is niet gevonden. Controleer of de webservice Hallo-Id juist is en probeer het opnieuw. |
| WorkspaceNotFound | De werkruimte is niet gevonden. Controleer of Hallo werkruimte-Id juist is en probeer het opnieuw. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (HTTP-statuscode 408)
 
Hallo-bewerking kan niet worden voltooid binnen de toegestane tijd Hallo.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| RequestCanceled | Aanvraag is geannuleerd door Hallo-client. |
| ScoreRequestTimeout | Er is een time-out opgetreden voor de aanvraag voor het uitvoeren. |
 
## <a name="conflict-http-status-code-409"></a>Conflict (HTTP-statuscode 409)
 
Er bestaat al een resource.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Ongeldige uitvoer parameternaam. Hallo metagegevens editor module toorename kolommen en probeer het opnieuw. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (HTTP-statuscode 413)
 
Hallo model had Hallo geheugenquotum toegewezen tooit overschreden.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| OutOfMemoryLimit | Hallo model verbruikt meer geheugen hebben dan is bestemd is voor deze. Maximaal toegestane hoeveelheid geheugen voor Hallo model is {0} MB. Controleer of het model voor problemen. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (HTTP-statuscode 500)
 
Uitvoering van een interne fout opgetreden.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | Hallo container proces gecrasht met systeemfout |
| ContainerProcessTerminatedWithUnknownError | Hallo container proces vastgelopen met een onbekende fout |
| ContainerValidationFailed | BLOB-container-validatie is mislukt vanwege de volgende fout: {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | Er zijn geen argumenten opgegeven. Controleer of dat de geldige argumenten zijn doorgegeven en probeer het opnieuw. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | Poort-id = {0} heeft een niet-ondersteund gegevenstype: {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Genereren van swagger is mislukt, Details: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | Onbekende taak statuscode {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage, Details: {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (HTTP-statuscode 500)
 
Uitvoering van een interne fout opgetreden. Het systeem is onvoldoende geheugen beschikbaar. Probeer het opnieuw.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (HTTP-statuscode 500)
 
Ongeldig modeltype pakket. Controleer of Hallo model pakket opgegeven juist is en probeer het opnieuw.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (HTTP-statuscode 500)
 
Ongeldige web service-pakket. Controleer of Hallo webpakket opgegeven juist is en probeer het opnieuw.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| ModuleError | Hallo web service pakket grafiek is ongeldig. Details: {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (HTTP-statuscode 503)
 
Hallo-aanvraag kan niet uitvoeren als Hallo containers worden geïnitialiseerd.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (HTTP-statuscode 503)
 
Service is tijdelijk niet beschikbaar.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| NoMoreResources | Er zijn geen bronnen beschikbaar zijn voor aanvraag. |
| RequestThrottled | Aanvraag is voor het eindpunt {0} beperkt. maximale gelijktijdigheid Hallo voor het Hallo-eindpunt is {1}. |
| TooManyConcurrentRequests | Te veel gelijktijdige aanvragen verzonden. |
| TooManyHostsBeingInitialized | Te veel hosts wordt geïnitialiseerd op Hallo dezelfde tijd. U kunt beperking / opnieuw uit te voeren. |
| TooManyHostsBeingInitializedPerModel | Te veel hosts wordt geïnitialiseerd op Hallo dezelfde tijd. U kunt beperking / opnieuw uit te voeren. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (HTTP-statuscode 504)
 
Hallo-bewerking kan niet worden voltooid binnen de toegestane tijd Hallo.
 
| Foutcode | Bericht van gebruiker |
| ---------- |--------------|
| BackendInitializationTimeout | Hallo web service-initialisatie kan niet worden voltooid binnen de toegestane tijd Hallo. |
| BackendScoreTimeout | uitvoeren van de Hallo web service-aanvraag kan niet worden voltooid binnen de toegestane tijd Hallo. |
 
