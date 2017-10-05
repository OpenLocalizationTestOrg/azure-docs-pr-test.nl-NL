---
title: Toepassingen publiceren naar afzonderlijke gebruikers in een Azure RemoteApp-verzameling (Preview) | Microsoft Docs
description: Lees hoe u in Azure RemoteApp apps naar afzonderlijke gebruikers kunt publiceren, in plaats van afhankelijk van groepen.
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a>Toepassingen publiceren naar afzonderlijke gebruikers in een Azure RemoteApp-verzameling (Preview)
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

In dit artikel wordt uitgelegd hoe u toepassingen publiceert voor afzonderlijke gebruikers in een Azure RemoteApp-verzameling. Dit is nieuwe functionaliteit in Azure RemoteApp, momenteel als Private Preview-versie beschikbaar voor vroege gebruikers (alleen voor evaluatiedoeleinden).

Oorspronkelijk konden toepassingen in Azure RemoteApp slechts op één manier worden gepubliceerd: de beheerder publiceerde apps vanuit de installatiekopie waarna ze zichtbaar waren voor alle gebruikers in de verzameling.

Een veelvoorkomend scenario is het opnemen van veel toepassingen in één installatiekopie en de implementatie van één verzameling om managementkosten te verlagen. Vaak zijn niet alle toepassingen relevant voor alle gebruikers, en zouden beheerders liever apps publiceren naar afzonderlijke gebruikers, zodat deze geen onnodige toepassingen in hun toepassingsfeed zien.

Dit is nu als een beperkte preview-functie mogelijk in Azure RemoteApp. Hier volgt een korte samenvatting van de nieuwe functionaliteit:

1. Een verzameling kan worden ingesteld op een van de volgende twee modi:
   
   * De oorspronkelijke verzamelmodus, waarbij alle gebruikers in een verzameling alle gepubliceerde toepassingen zien. Dit is de standaardmodus.
   * De nieuwe toepassingsmodus, waarin gebruikers alleen de toepassingen zien die aan hen zijn toegewezen
2. Op het moment kan de toepassingsmodus alleen worden ingeschakeld met PowerShell-cmdlets van Azure RemoteApp.
   
   * Als de verzameling is ingesteld op de toepassingsmodus, kan gebruikerstoewijzing in de verzameling niet worden beheerd via de Azure-portal. Gebruikerstoewijzing moet worden beheerd via de PowerShell-cmdlets.
3. Gebruikers zien alleen de toepassingen die rechtstreeks aan hen zijn gepubliceerd. Een gebruiker heeft echter nog steeds de mogelijkheid om de andere toepassingen te starten die beschikbaar zijn in de installatiekopie, door deze rechtstreeks in het besturingssysteem te starten.
   
   * Deze functie biedt geen veilige vergrendeling van toepassingen maar beperkt alleen de zichtbaarheid in de toepassingsfeed.
   * Als u gebruikers van toepassingen wilt isoleren, moet u daar afzonderlijke verzamelingen voor gebruiken.

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a>PowerShell-cmdlets van Azure RemoteApp ophalen
Als u de nieuwe preview-functionaliteit wilt uitproberen, moet u Azure PowerShell-cmdlets gebruiken. Het is momenteel niet mogelijk om de nieuwe toepassingspublicatiemodus in te schakelen met Azure Management Portal.

Controleer eerst of de [Azure PowerShell-module](/powershell/azure/overview) is geïnstalleerd.

Start daarna de PowerShell-console in de beheerdersmodus en voer de volgende cmdlet uit:

        Add-AzureAccount

U wordt gevraagd naar uw Azure-gebruikersnaam en -wachtwoord. Wanneer u bent aangemeld, kunt u Azure RemoteApp-cmdlets uitvoeren binnen uw Azure-abonnementen.

## <a name="how-to-check-which-mode-a-collection-is-in"></a>Controleren welke modus voor een verzameling is ingeschakeld
Voer de volgende cmdlet uit:

        Get-AzureRemoteAppCollection <collectionName>

![De verzamelmodus controleren](./media/remoteapp-perapp/araacllelvel.png)

De eigenschap AclLevel kan de volgende waarden hebben:

* Verzameling: De oorspronkelijke publicatiemodus. Alle gebruikers zien alle gepubliceerde apps.
* Toepassing: De nieuwe publicatiemodus. Gebruikers zien alleen de apps die rechtstreeks naar hen zijn gepubliceerd.

## <a name="how-to-switch-to-application-publishing-mode"></a>Overschakelen naar toepassingspublicatiemodus
Voer de volgende cmdlet uit:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Toepassingspublicatiestatus blijft behouden: in eerste instantie zien alle gebruikers alle oorspronkelijke gepubliceerde apps.

## <a name="how-to-list-users-who-can-see-a-specific-application"></a>Een lijst weergeven van gebruikers die een specifieke toepassing kunnen zien
Voer de volgende cmdlet uit:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Hiermee wordt een lijst weergegeven van alle gebruikers die de toepassing kunnen zien.

Opmerking: u kunt de toepassingsaliassen (in de bovenstaande syntaxis 'app alias' genoemd) zien door Get-AzureRemoteAppProgram - CollectionName <collectionName> uit te voeren.

## <a name="how-to-assign-an-application-to-a-user"></a>Een toepassing toewijzen aan een gebruiker
Voer de volgende cmdlet uit:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

De gebruiker ziet nu de toepassing in de Azure RemoteApp-client en kan hiermee verbinding maken.

## <a name="how-to-remove-an-application-from-a-user"></a>Een toepassing verwijderen van een gebruiker
Voer de volgende cmdlet uit:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Feedback geven
We waarderen uw feedback en suggesties met betrekking tot deze preview-functie. Zou u de [enquête](http://www.instant.ly/s/FDdrb) willen invullen om ons te laten weten wat u ervan vindt?

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a>Hebt u nog geen gelegenheid gehad om de preview-functie uit te proberen?
Als u nog niet hebt deelgenomen aan de preview, kunt u deze [enquête](http://www.instant.ly/s/AY83p) gebruiken om toegang aan te vragen.

