---
title: een Azure storage-account met Azure CDN aaaIntegrate | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure inhoud Delivery Network (CDN) toodeliver hoge bandbreedte inhoud door het in cache plaatsen van Azure Storage-blobs.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Een Azure storage-account integreren met Azure CDN
CDN kan worden ingeschakeld toocache inhoud in uw Azure-opslag. Het biedt ontwikkelaars een globale oplossing voor hoge bandbreedte inhoud leveren door blobs en statische inhoud van de compute-exemplaren op fysieke knooppunten op Hallo Verenigde Staten, Europa, Azië, Australië en Zuid-Amerika cache te plaatsen.

## <a name="step-1-create-a-storage-account"></a>Stap 1: Een opslagaccount maken
Hallo te volgen procedure toocreate een nieuw opslagaccount voor een Azure-abonnement gebruiken. Een opslagaccount biedt toegang tot Azure storage-services. Hallo storage-account vertegenwoordigt Hallo hoogste niveau van Hallo naamruimte voor het openen van elk van de onderdelen van een hello Azure storage-service: Blob-services, wachtrijservices en services van de tabel. Raadpleeg voor meer informatie, toohello [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md).

toocreate een opslagaccount, moet u Hallo servicebeheerder of medebeheerder voor Hallo gekoppeld abonnement.

> [!NOTE]
> Er zijn verschillende methoden kunt u toocreate storage-account, inclusief hello Azure-Portal en Powershell.  Voor deze zelfstudie worden gebruikt hello Azure-Portal.  
> 
> 

**toocreate een opslagaccount voor een Azure-abonnement**

1. Meld u aan toohello [Azure Portal](https://portal.azure.com).
2. Selecteer in de linkerbovenhoek Hallo **nieuw**. In Hallo **nieuw** dialoogvenster **gegevens en opslag**, klikt u vervolgens op **opslagaccount**.
    
    Hallo **storage-account maken** blade wordt weergegeven.   

    ![Storage-Account maken][create-new-storage-account]  

3. In Hallo **naam** veld, typt u de subdomeinnaam. Deze vermelding kan 3 tot 24 kleine letters en cijfers bevatten.
   
    Deze waarde wordt Hallo hostnaam binnen Hallo URI die wordt gebruikt om Blob, wachtrij of tabel resources voor Hallo-abonnement. Om een containerresource in Hallo Blob-service op te lossen, gebruikt u een URI in Hallo-indeling te volgen waarbij  *&lt;StorageAccountLabel&gt;*  toohello-waarde die u hebt getypt in verwijst **Voer een URL**:
   
    http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*
   
    **Belangrijk:** Hallo URL label formulieren Hallo subdomein van het opslagaccount Hallo URI en moet uniek zijn alle gehoste services in Azure.
   
    Deze waarde wordt ook gebruikt als Hallo-naam van dit opslagaccount in de portal Hallo of bij het openen van dit account via een programma.
4. Laat de standaardwaarden voor Hallo **implementatiemodel**, **Account kind**, **prestaties**, en **replicatie**. 
5. Selecteer Hallo **abonnement** Hallo storage-account wordt gebruikt met.
6. Selecteer of maak een **resourcegroep**.  Zie [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.
7. Selecteer een locatie voor uw opslagaccount.
8. Klik op **Create**. Hallo-proces voor het maken van Hallo storage-account kan toocomplete van enkele minuten duren.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Stap 2: CDN inschakelen voor Hallo storage-account

Met de nieuwste integratie hello, kunt u nu CDN inschakelen voor uw opslagaccount zonder de uitbreiding van uw storage-portal. 

1. Selecteer Hallo opslagaccount, 'CDN' of blader naar beneden zoeken in Hallo linkernavigatievenster menu aan en klik vervolgens op 'Azure CDN'.
    
    Hallo **Azure CDN** blade wordt weergegeven.

    ![CDN inschakelen navigatie][cdn-enable-navigation]
    
2. Maak een nieuwe eindpunt Hallo vereist gegevens invoeren
    - **CDN-profiel**: U kunt een nieuwe maken of een bestaand profiel gebruiken.
    - **Prijscategorie**: U hoeft alleen tooselect een prijscategorie als u een nieuw CDN-profiel maakt.
    - **De naam van de CDN-eindpunt**: Voer de naam van een eindpunt per uw keuze.

    > [!TIP]
    > CDN-eindpunt gemaakt Hallo standaard Hallo hostnaam van uw storage-account als oorsprong.

    ! [cdn-eindpunt maken van nieuwe] [cdn--eindpunt-maken van nieuwe]

3. Na het maken, wordt nieuw Hallo-eindpunt weergegeven in bovenstaande Hallo endpoint-lijst.

    ![storage-nieuwe CDN-eindpunt][cdn-storage-new-endpoint]

> [!NOTE]
> U kunt ook tooAzure CDN extensie tooenable CDN gaan. [Zelfstudie](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>Stap 3: Extra CDN-functies inschakelen

Klik in de 'Azure CDN' blade opslagaccount Hallo CDN-eindpunt op Hallo lijst tooopen CDN configuratie blade. U kunt aanvullende CDN-functies inschakelen voor uw levering, zoals compressie, queryreeks geo filteren. U kunt ook aangepaste domein toewijzing tooyour CDN-eindpunt toevoegen en inschakelen van aangepast domein HTTPS.
    
![CDN-opslagconfiguratie cdn][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>Stap 4: Toegang tot CDN-inhoud
tooaccess in de cache inhoud op CDN hello, gebruik Hallo CDN-URL opgegeven in Hallo-portal. Hallo-adres voor een blob-cache is vergelijkbaar toohello volgende:

http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]
> Wanneer u CDN toegang tooa storage-account hebt ingeschakeld, zijn alle openbaar beschikbare objecten in aanmerking komen voor CDN edge cache. Als u een object dat momenteel in cache in Hallo CDN wijzigt, wordt Hallo nieuwe inhoud pas beschikbaar via Hallo CDN Hallo CDN wordt de inhoud vernieuwd wanneer Hallo in de cache opgeslagen inhoud time-to-live-periode is verstreken.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>Stap 5: Verwijder de inhoud uit CDN Hallo
Als u niet langer wenst toocache een object in hello Azure Content Delivery Network (CDN), kunt u een van de volgende stappen uit Hallo uitvoeren:

* Kunt u Hallo private in plaats van een openbare container. Zie [anonieme leestoegang toocontainers en blobs beheren](../storage/blobs/storage-manage-access-to-resources.md) voor meer informatie.
* U kunt uitschakelen of verwijderen van Hallo CDN-eindpunt met behulp van Hallo-beheerportal.
* U kunt uw gehoste service toono langer reageren toorequests voor Hallo object wijzigen.

Een object dat al in de cache in Hallo CDN blijft in cache totdat Hallo time to live voor Hallo-object zijn verstreken of Hallo-eindpunt wordt verwijderd. Wanneer Hallo time-to-live-periode is verstreken, controleert Hallo CDN toosee of Hallo CDN-eindpunt nog geldig is en Hallo-object is nog steeds anoniem toegankelijk. Als dit niet het geval is, klikt u vervolgens Hallo-object wordt niet langer in de cache.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Hoe tooMap CDN inhoud tooa aangepaste domeinen](cdn-map-content-to-custom-domain.md)
* [HTTPS inschakelen voor uw aangepaste domein](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
