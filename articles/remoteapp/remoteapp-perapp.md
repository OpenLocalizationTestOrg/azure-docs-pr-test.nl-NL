---
title: aaaPublish toepassingen tooindividual gebruikers in een Azure RemoteApp-verzameling (Preview) | Microsoft Docs
description: Meer informatie over hoe u apps tooindividual gebruikers, in plaats van kunt publiceren, afhankelijk van groepen in Azure RemoteApp.
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
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Publiceren van toepassingen tooindividual gebruikers in een Azure RemoteApp-verzameling (Preview)
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Dit artikel wordt uitgelegd hoe toopublish toepassingen tooindividual gebruikers in een Azure RemoteApp-verzameling. Dit is nieuwe functionaliteit in Azure RemoteApp, momenteel in Preview-versie private en vroege gebruikers beschikbaar alleen tooselect voor evaluatiedoeleinden.

Oorspronkelijk Azure RemoteApp slechts op één manier van publicatie van toepassingen ingeschakeld: Hallo beheerder publiceerde apps vanuit Hallo installatiekopie waarna ze zichtbaar tooall gebruikers in Hallo-verzameling.

Een gebruikelijk scenario is tooinclude veel toepassingen in één installatiekopie en het implementeren van een verzameling in volgorde tooreduce beheerkosten. Vaak zijn niet alle toepassingen zijn relevante tooall gebruikers – beheerders liever toopublish apps tooindividual gebruikers zodat ze geen onnodige toepassingen in hun toepassingsfeed zien.

Dit is nu als een beperkte preview-functie mogelijk in Azure RemoteApp. Hier volgt een korte samenvatting van de nieuwe functionaliteit Hallo:

1. Een verzameling kan worden ingesteld op een van de volgende twee modi:
   
   * Hallo oorspronkelijke Verzamelmodus alle gebruikers in een verzameling zien gepubliceerde alle toepassingen. Dit is de standaardmodus Hallo.
   * Hallo nieuwe toepassingsmodus, waar gebruikers alleen de toepassingen zien die expliciet zijn toegewezen toothem
2. Hallo momenteel kan Hallo toepassingsmodus alleen worden ingeschakeld met behulp van Azure RemoteApp-PowerShell-cmdlets.
   
   * Wanneer de modus instellen voor tooapplication, Gebruikerstoewijzing in Hallo verzameling kan niet worden beheerd via hello Azure-portal. Gebruikerstoewijzing heeft toobe beheerd via de PowerShell-cmdlets.
3. Gebruikers zien alleen Hallo toepassingen rechtstreeks toothem gepubliceerd. Echter nog steeds mogelijk voor een gebruiker toolaunch andere toepassingen die beschikbaar zijn op de installatiekopie Hallo Hallo door deze rechtstreeks in Hallo-besturingssysteem.
   
   * Deze functie biedt geen veilige vergrendeling van toepassingen. beperkt alleen de zichtbaarheid in Hallo toepassingsfeed.
   * Als u gebruikers tooisolate van toepassingen moet, moet u toouse afzonderlijke verzamelingen voor die.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>Hoe tooget Azure RemoteApp-PowerShell-cmdlets
tootry hello nieuwe preview-functionaliteit, moet u toouse Azure PowerShell-cmdlets. Het is momenteel niet mogelijk toouse hello Azure Management portal tooenable Hallo nieuwe toepassingspublicatiemodus.

Controleer eerst of er Hallo [Azure PowerShell-module](/powershell/azure/overview) geïnstalleerd.

Start vervolgens Hallo PowerShell-console in de beheerdersmodus en Voer Hallo volgende cmdlet:

        Add-AzureAccount

U wordt gevraagd naar uw Azure-gebruikersnaam en -wachtwoord. Nadat u bent aangemeld, kunt u zich kunt toorun Azure RemoteApp-cmdlets op basis van uw Azure-abonnementen.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>Hoe toocheck welke modus een verzameling bevindt zich in
Voer Hallo volgende cmdlet:

        Get-AzureRemoteAppCollection <collectionName>

![Hallo Verzamelmodus controleren](./media/remoteapp-perapp/araacllelvel.png)

Hallo eigenschap AclLevel kan Hallo volgende waarden hebben:

* Verzameling: Hallo oorspronkelijke publicatiemodus. Alle gebruikers zien alle gepubliceerde apps.
* Toepassing: Hallo nieuwe publicatiemodus. Gebruikers zien alleen de apps Hallo rechtstreeks toothem gepubliceerd.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>Hoe tooswitch tooapplication publicatiemodus
Voer Hallo volgende cmdlet:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Toepassingspublicatiestatus blijft behouden: in eerste instantie zien alle gebruikers alle oorspronkelijke gepubliceerde apps Hallo.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Hoe toolist-gebruikers die een specifieke toepassing kunnen zien
Voer Hallo volgende cmdlet:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Hiermee worden alle gebruikers die de toepassing hello kunnen zien.

Opmerking: U kunt Hallo toepassingsaliassen ('app alias' in de bovenstaande syntaxis voor Hallo genoemd) zien door het uitvoeren van Get-AzureRemoteAppProgram - CollectionName <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>Hoe een gebruiker van toepassing tooa tooassign
Voer Hallo volgende cmdlet:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

Hallo gebruiker ziet nu de toepassing hello in hello Azure RemoteApp-client en kunnen tooconnect tooit zijn.

## <a name="how-tooremove-an-application-from-a-user"></a>Hoe een toepassing van een gebruiker tooremove
Voer Hallo volgende cmdlet:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Feedback geven
We waarderen uw feedback en suggesties met betrekking tot deze preview-functie. Vul Hallo [enquête](http://www.instant.ly/s/FDdrb) toolet ons weten wat u denkt.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>Dit nog niet hebt gehad kans tootry Hallo preview-functie?
Als u nog niet hebt deelgenomen Hallo Preview nog, gebruik dit [enquête](http://www.instant.ly/s/AY83p) toorequest toegang.

