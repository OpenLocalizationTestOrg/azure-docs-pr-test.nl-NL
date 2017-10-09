---
title: gebruik van aaaImplement disaster recovery back-up en herstel in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toouse back-up en noodherstel tooperform in Azure API Management te herstellen.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Hoe gebruik van tooimplement disaster recovery service back-up en herstellen in Azure API Management
Door toopublish kiezen en beheren van uw API's via Azure API Management u van veel fout tolerantie en infrastructuur mogelijkheden die hebt u anders toodesign profiteert, implementeren en beheren. Hello Azure-platform vermindert een groot deel van mogelijke fouten in een fractie van Hallo kosten.

toorecover van beschikbaarheidsproblemen bij het Hallo-regio waar uw API Management-service is gehost u moet op elk gewenst moment op gereed tooreconstitute uw service in een andere regio zijn. Afhankelijk van uw doelstellingen van de beschikbaarheid en de beoogde hersteltijd mogelijk u wilt dat tooreserve een Backup-service in een of meer regio's en probeer het toomaintain hun configuratie en -inhoud gesynchroniseerd met de Hallo actieve service. Hallo service back-up en herstelfunctie nodig bouwsteen Hallo biedt voor het implementeren van uw strategie voor noodherstel.

Deze handleiding wordt getoond hoe tooauthenticate Azure Resource Manager-aanvragen en hoe toobackup en herstellen van uw API Management-service-exemplaren.

> [!NOTE]
> Hallo-proces voor een back-up en herstellen van een API Management-service-exemplaar voor herstel na noodgevallen kan ook worden gebruikt voor het repliceren van exemplaren van API Management-service voor scenario's zoals fasering.
>
> Houd er rekening mee dat elke back-up na 30 dagen verloopt. Als u een back-up toorestore probeert nadat de vervalperiode van Hallo 30 dagen is verlopen, Hallo herstellen mislukt met een `Cannot restore: backup expired` bericht.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Verificatie van Azure Resource Manager-aanvragen
> [!IMPORTANT]
> Hallo REST-API voor back-up en herstel gebruikt Azure Resource Manager en heeft een ander verificatiemechanisme dan Hallo REST-API's voor het beheren van uw API Management-entiteiten. Hallo stappen in deze sectie wordt beschreven hoe tooauthenticate Azure Resource Manager-aanvragen. Zie voor meer informatie [verificatie van Azure Resource Manager-aanvragen](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Alle Hallo-taken die u doen op resources met behulp van hello Azure Resource Manager moeten worden geverifieerd met Azure Active Directory met Hallo stappen te volgen.

* Toevoegen van een toepassing toohello Azure Active Directory-tenant.
* Stel de machtigingen voor Hallo-toepassing die u hebt toegevoegd.
* Hallo-token ophalen voor het verifiëren van aanvragen tooAzure Resource Manager.

de eerste stap Hallo is toocreate een Azure Active Directory-toepassing. Meld u aan bij Hallo [klassieke Azure-Portal](http://manage.windowsazure.com/) met Hallo-abonnement met uw API Management-service-instantie en navigeer toohello **toepassingen** tabblad voor uw standaard Azure Active Directory.

> [!NOTE]
> Als de standaarddirectory voor hello Azure Active Directory is niet zichtbaar tooyour account, vereist contact op met Hallo beheerder hello Azure-abonnement toogrant Hallo tooyour account met machtigingen.

![Azure Active Directory-toepassing maken][api-management-add-aad-application]

Klik op **toevoegen**, **mijn organisatie ontwikkelt toepassing toevoegen**, en kies **Native client-toepassing**. Voer een beschrijvende naam en klik op volgende pijl Hallo. Geef een tijdelijke aanduiding-URL, zoals `http://resources` voor Hallo **omleidings-URI**, zoals dit een verplicht veld is, maar Hallo-waarde is niet later gebruikt. Klik op Hallo selectievakje toosave Hallo toepassing.

Nadat de toepassing hello wordt opgeslagen, klikt u op **configureren**, schuif omlaag toohello **machtigingen tooother toepassingen** sectie en op **toepassing toevoegen**.

![Machtigingen toevoegen][api-management-aad-permissions-add]

Selecteer **Windows** **Azure Service Management API** en klik op Hallo selectievakje tooadd Hallo toepassing.

![Machtigingen toevoegen][api-management-aad-permissions]

Klik op **gedelegeerde machtigingen** naast Hallo toegevoegde **Windows** **Azure Service Management API** toepassing hello selectievakje voor **Access Azure Service Management (preview)**, en klik op **opslaan**.

![Machtigingen toevoegen][api-management-aad-delegated-permissions]

Eerdere tooinvoking Hallo API's die genereren Hallo back-up en herstel hem, is het nodig tooget een token. Hallo volgende voorbeeld wordt Hallo [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget-pakket tooretrieve Hallo-token.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Vervang `{tentand id}`, `{application id}`, en `{redirect uri}` met Hallo instructies te volgen.

Vervang `{tenant id}` met tenant-id Hallo Hallo Azure Active Directory-toepassing die u zojuist hebt gemaakt. U kunt toegang krijgen tot Hallo-id door te klikken op **eindpunten weergeven**.

![Eindpunten][api-management-aad-default-directory]

![Eindpunten][api-management-endpoint]

Vervang `{application id}` en `{redirect uri}` met Hallo **Client-Id** en de URL van Hallo Hallo **omleidings-URI's** gedeelte van uw Azure Active Directory-toepassing **configureren**  tabblad.

![Resources][api-management-aad-resources]

Wanneer het Hallo-waarden zijn opgegeven, weer Hallo codevoorbeeld een token vergelijkbare toohello voorbeeld te volgen.

![Token][api-management-arm-token]

Stel voordat aanroepen Hallo back-up en herstelbewerkingen die zijn beschreven in de volgende secties Hallo, Hallo autorisatie aanvraag-header voor de REST-aanroep.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"></a>Back-up van een API Management-service
tooback van een API Management-service probleem Hallo HTTP-aanvraag te volgen:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

Waarbij:

* `subscriptionId`-id van het Hallo-abonnement met API Management-service Hallo u toobackup probeert
* `resourceGroupName`-een tekenreeks in de vorm van 'Api - standaard-{service regio}' hello waar `service-region` identificeert hello Azure-regio waar Hallo API Management-service die u probeert toobackup wordt gehost, bijvoorbeeld`North-Central-US`
* `serviceName`-naam Hallo Hallo van een back-up van opgegeven Hallo gelijktijdig met het maken maken van API Management-service
* `api-version`-vervangen`2014-02-14`

Geef in de hoofdtekst van de Hallo van Hallo aanvraag, Hallo doel-Azure-opslag-accountnaam, toegangssleutel, de naam van de blob-container en back-upnaam:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Hallo-waarde van Hallo `Content-Type` aanvraagheader te`application/json`.

Back-up is een langdurige bewerking die toocomplete van meerdere minuten kan duren.  Als Hallo-aanvraag voltooid is en Hallo back-upproces is gestart. u ontvangt een `202 Accepted` statuscode van antwoord met een `Location` header.  Controleer 'GET-aanvragen toohello URL in Hallo `Location` header toofind Hallo status van Hallo-bewerking. U blijft tooreceive '202 geaccepteerd' statuscode terwijl Hallo back-up uitgevoerd wordt. Reactiecode `200 OK` geven aan welke Hallo back-upbewerking is voltooid.

Houd er rekening mee Hallo volgen beperkingen bij het maken van een back-aanvraag.

* **Container** opgegeven in de aanvraagtekst Hallo **moet bestaan**.
* Terwijl back-up uitgevoerd u wordt **moet niet proberen deze service management bewerkingen** zoals SKU upgrade of een downgrade, wijziging van de domeinnaam, enzovoort.
* Herstellen van een **back-up kan worden gegarandeerd alleen voor 30 dagen** sinds het moment Hallo van het maken ervan.
* **Gebruiksgegevens** gebruikt voor het analytics-Rapporten maken **wordt niet meegeleverd** in Hallo back-up. Gebruik [REST-API van Azure API Management] [ Azure API Management REST API] tooperiodically ophalen analytics-Rapporten voor veilig te bewaren.
* Hallo frequentie waarmee u de service back-ups uitvoeren heeft invloed op uw beoogd herstelpunt. toominimize deze geadviseerd de uitvoering van regelmatige back-ups als back-ups op aanvraag uitvoeren nadat u belangrijke wijzigingen tooyour API Management-service.
* **Wijzigingen** en-klare toohello van serviceconfiguratie (bijvoorbeeld API's, beleid, developer portal vormgeving) tijdens het back-upbewerking wordt uitgevoerd **worden mogelijk niet opgenomen in Hallo back-up en daarom gaan verloren**.

## <a name="step2"></a>Herstellen van een API Management-service
toorestore een API Management-service van een eerder gemaakte back-up maken Hallo HTTP-aanvraag te volgen:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

Waarbij:

* `subscriptionId`-id van het Hallo-abonnement met Hallo herstelt u een back-up in API Management-service
* `resourceGroupName`-een tekenreeks in de vorm van 'Api - standaard-{service regio}' hello waar `service-region` identificeert hello Azure-regio waar Hallo herstelt u een back-up in API Management-service wordt gehost, bijvoorbeeld`North-Central-US`
* `serviceName`-naam Hallo Hallo API Management-service wordt hersteld in bij Hallo van het maken ervan worden opgegeven
* `api-version`-vervangen`2014-02-14`

Geef in de hoofdtekst van de Hallo van Hallo aanvraag, Hallo back-upbestand locatie, dat wil zeggen accountnaam van de Azure-opslag, toegangssleutel, de naam van de blob-container en back-upnaam:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Hallo-waarde van Hallo `Content-Type` aanvraagheader te`application/json`.

Terugzetten is een langdurige bewerking die voordat too30 of meer minuten toocomplete duren kan.  Als Hallo-aanvraag voltooid is en herstelproces Hallo is gestart. u ontvangt een `202 Accepted` statuscode van antwoord met een `Location` header.  Controleer 'GET-aanvragen toohello URL in Hallo `Location` header toofind Hallo status van Hallo-bewerking. U blijft tooreceive '202 geaccepteerde' statuscode terwijl Hallo terugzetten uitgevoerd wordt. Reactiecode `200 OK` geven aan welke Hallo restore-bewerking is voltooid.

> [!IMPORTANT]
> **Hallo SKU** van Hallo-service wordt hersteld in **moet overeenkomen met** Hallo SKU Hallo een back-up service wordt hersteld.
>
> **Wijzigingen** en-klare toohello van serviceconfiguratie (bijvoorbeeld API's, beleid, developer portal vormgeving) tijdens een herstelbewerking wordt uitgevoerd **kunnen worden overschreven**.
>
>

## <a name="next-steps"></a>Volgende stappen
Uitchecken Hallo-blogs van Microsoft voor twee verschillende scenario's van de back-up-/ herstelproces hello te volgen.

* [Azure API Management Accounts repliceren](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * Bedankt dat u tooGisela voor haar bijdrage toothis artikel.
* [Azure API Management: Een back-Up en herstellen van de configuratie](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * Hallo benadering gedetailleerde door Stuart komt niet overeen met de officiële richtlijnen hello, maar het is heel interessant.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
