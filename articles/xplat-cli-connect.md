---
title: aaaLog in tooAzure van Hallo CLI | Microsoft Docs
description: Azure-abonnement tooyour vanaf hello Azure-opdrachtregelinterface (Azure CLI) verbinding te maken voor Mac, Linux en Windows
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>Meld u bij tooAzure van hello Azure CLI
Hello Azure CLI is een set van open-source, platformoverschrijdende opdrachten voor het werken met Azure-resources. Dit artikel wordt beschreven Hallo verschillende manieren tooprovide Azure-account referenties tooconnect hello Azure CLI tooyour Azure-abonnement:

* Voer Hallo `azure login` CLI opdracht tooauthenticate via Azure Active Directory. Deze methode biedt u toegang tot de opdrachten tooCLI in beide [opdracht modi](#cli-command-modes). Wanneer u de opdracht Hallo zonder extra opties uitvoert `azure login` vraagt u toocontinue interactief aanmelden via een webportal. Voor extra `azure login` opdracht Opties, Zie Hallo scenario's in dit artikel of type `azure login --help`.
* Als u moet alleen toouse Azure Service Management modus CLI-opdrachten (niet aanbevolen voor de meeste nieuwe implementaties), kunt u downloaden en installeren van een bestand met instellingen publiceren op uw computer.

Als u nog niet Hallo CLI hebt geïnstalleerd, raadpleegt u [installeren hello Azure CLI](cli-install-nodejs.md). Als u geen Azure-abonnement hebt, kunt u binnen een paar minuten een [gratis account](http://azure.microsoft.com/free/) maken.

Zie voor achtergrondinformatie over andere account-id's en Azure-abonnementen [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Scenario 1: azure-aanmelding met interactieve aanmelding
Met bepaalde accounts Hallo CLI, moet u toorun `azure login` en ga vervolgens door Hallo aanmelding met een webbrowser via een webportal, een proces genaamd *interactieve aanmelding*. Een veelvoorkomende reden is wanneer u een account voor werk of school hebt (ook wel een *organisatieaccount*) die toorequire multifactor-verificatie is ingesteld. Ook interactieve aanmelding met je Microsoft-account gebruiken als u wilt dat de opdrachten in de modus Resource Manager toouse.

Interactieve aanmelding is eenvoudig: type `azure login` --zonder opties--zoals weergegeven in Hallo voorbeeld te volgen:

```
azure login
```                                                                                             

Hallo-uitvoer wordt weergegeven dat lijkt op Hallo volgende:

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Hallo-code die worden aangeboden tooyou in de opdrachtuitvoer Hallo kopiëren en open een browser toohttp://aka.ms/devicelogin of een andere pagina als opgegeven. (U kunt een browser op Hallo openen dezelfde computer of op een andere computer of apparaat.) Hallo-code invoeren, en vervolgens u na vragen aan gebruiker tooenter Hallo gebruikersnaam en wachtwoord voor de identiteit van de Hallo gewenste toouse. Wanneer dit proces is voltooid, geeft opdrachtshell Hallo Hallo aanmelding is voltooid. Dit kan als volgt uitzien:

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> Met interactieve aanmelding, worden verificatie en autorisatie uitgevoerd met Azure Active Directory. Als u de identiteit van een Microsoft-account gebruikt, heeft uw Azure Active Directory-standaarddomein toegang tot Hallo-aanmelding. (Als u zich aangemeld voor een gratis Azure-account, Azure Active Directory automatisch gemaakt een standaarddomein voor uw account.)
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>Scenario 2: azure-aanmelding met een gebruikersnaam en wachtwoord
Gebruik Hallo `azure login` opdracht met Hallo gebruikersnaam (`-u`) parameter tooauthenticate wanneer u wilt dat toouse een werk- of schoolaccount die geen multifactor-verificatie vereist. U wordt gevraagd op de opdrachtregel Hallo Hallo wachtwoord (of u kunt eventueel Hallo wachtwoord doorgeven als een extra parameter Hallo `azure login` opdracht). Hallo volgende voorbeeld wordt doorgegeven Hallo gebruikersnaam van een organisatie-account:

    azure login -u myUserName@contoso.onmicrosoft.com

U bent vervolgens tooenter gevraagd uw wachtwoord:

    info:    Executing command login
    Password: *********

Hallo-aanmelding wordt voltooid.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

Als dit de eerste keer aangemeld met deze referenties is, wordt u gevraagd tooverify dat u toocache geen verificatietoken wenst. Deze vraag vindt ook plaats als u eerder hebt gebruikt Hallo `azure logout` opdracht (beschreven in artikel hello later). toobypass deze prompt voor automatiseringsscenario's uitgevoerd `azure login` Hello `-q` parameter.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Scenario 3: azure-aanmelding met een service-principal
Als u een service-principal voor een Active Directory-toepassing maakt en service-principal Hallo machtigingen op uw abonnement heeft, kunt u Hallo `azure login` opdracht tooauthenticate Hallo service-principal. Afhankelijk van uw scenario kan u referenties van de service-principal Hallo Hallo opgeven als expliciete parameters Hallo `azure login` opdracht. Bijvoorbeeld: hello volgende opdracht wordt doorgegeven Hallo service principal name en Active Directory-tenant-ID:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

U bent na vragen aan gebruiker tooprovide Hallo wachtwoord. U kunt ook Hallo referenties via een CLI script of toepassing code, of gebruik een certificaat tooauthenticate Hallo service-principal niet-interactief voor automatiseringsscenario's. Zie voor meer informatie en voorbeelden [verifiëren van een service-principal met Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Scenario 4: Gebruik een bestand met publicatie-instellingen
Als u moet alleen toouse hello Azure Service Management modus CLI-opdrachten (bijvoorbeeld toodeploy Azure VM's in het klassieke implementatiemodel Hallo), kunt u verbinding maken met behulp van een bestand met publicatie-instellingen. Deze methode wordt een certificaat geïnstalleerd op uw lokale computer waarmee u beheertaken tooperform voor zolang Hallo-abonnement en het Hallo-certificaat geldig zijn.

* **Hallo toodownload bestand publicatie-instellingen** Zorg ervoor dat Hallo CLI in Service Management-modus door in te voeren is voor uw account `azure config mode asm`. Voer vervolgens de volgende opdracht Hallo:

        azure account download

Hiermee opent u de standaardbrowser en vraagt u toosign in toohello [klassieke Azure-portal](https://manage.windowsazure.com). Nadat u zich aanmeldt, een `.publishsettings` bestand downloads. Noteer waar dit bestand wordt opgeslagen.

> [!NOTE]
> Als uw account gekoppeld aan meerdere tenants van Azure Active Directory is, hebt u mogelijk na vragen aan gebruiker tooselect die Active Directory die u wenst toodownload publicatie-instellingen voor het bestand.
>
>

Wanneer met behulp van de downloadpagina Hallo of via de klassieke Azure-portal Hallo wordt Hallo geselecteerde Active Directory Hallo standaardwaarde gebruikt door de klassieke portal Hallo en downloadpagina. Nadat een standaard is ingesteld, ziet u de tekst hello '**Klik hier tooreturn toohello selectiepagina**' hello boven aan het Hallo-downloadpagina. Hallo opgegeven koppeling tooreturn toohello selectiepagina gebruiken.

* **Hallo tooimport bestand publicatie-instellingen**, voert hello volgende opdracht:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> Na het importeren van de publicatie-instellingen, verwijdert u Hallo `.publishsettings` bestand. Het is niet langer vereist voor hello Azure CLI en vormt een beveiligingsrisico, omdat als het gebruikte toogain toegang tooyour abonnement mogelijk.
>
>

## <a name="cli-command-modes"></a>CLI-opdrachtmodi
Hello Azure CLI biedt twee opdrachtmodi voor het werken met Azure-resources met andere opdrachtsets:

* **Resource Manager-modus** : voor het werken met Azure-resources in Hallo Resource Manager-implementatiemodel. tooset deze modus wordt uitgevoerd `azure config mode arm`.
* **Service Management-modus** : voor het werken met Azure-resources in het klassieke implementatiemodel Hallo. tooset deze modus wordt uitgevoerd `azure config mode asm`.

Toen geïnstalleerd, Hallo huidige release van Hallo die CLI bevindt zich in de modus Resource Manager.

> [!NOTE]
> Hallo Resource Manager en Service Management-modus elkaar wederzijds uit. Dat wil zeggen, resources die zijn gemaakt in de modus voor één kunnen niet worden beheerd vanaf Hallo andere modus.
>
>

## <a name="multiple-subscriptions"></a>Meerdere abonnementen
Als u meerdere Azure-abonnementen hebt, verleent toegang tooall abonnementen die zijn gekoppeld aan uw referenties als u tooAzure verbinding te maken. Een abonnement is Hallo standaard geselecteerd en gebruikt door hello Azure CLI bij het uitvoeren van bewerkingen. Vindt u Hallo abonnementen, met inbegrip van de huidige standaardabonnement hello, met behulp van Hallo `azure account list` opdracht. Met deze opdracht retourneert informatie vergelijkbare toohello volgende:

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

Hallo in Hallo voorafgaand aan de lijst, **huidige** kolom wordt aangegeven Hallo huidige standaardabonnement als Azure-sub-1. toochange hello standaardabonnement, gebruik Hallo `azure account set` opdracht in en geef Hallo-abonnement dat u wenst dat toobe Hallo standaard. Bijvoorbeeld:

    azure account set Azure-sub-2

Hiermee wijzigt u Hallo standaard abonnement tooAzure-sub-2.

> [!NOTE]
> Hallo standaardabonnement wijzigen wordt direct van kracht en is een algemene wijziging; nieuwe Azure CLI-opdrachten, of u deze uit uitvoeren Hallo dezelfde opdrachtregelprogramma exemplaar of een ander exemplaar, nieuwe standaardabonnement hello gebruiken.
>
>

Als u toouse een niet-standaard-abonnement met hello Azure CLI wilt, maar niet dat toochange Hallo huidige standaard wilt, kunt u Hallo `--subscription` optie voor de opdracht Hallo en geef Hallo Hallo-abonnement dat u wenst dat toouse voor Hallo-bewerking.

Wanneer u verbonden tooyour Azure-abonnement bent, kunt u beginnen met behulp van hello Azure CLI-opdrachten toowork met Azure-resources.

## <a name="storage-of-cli-settings"></a>Opslag van CLI-instellingen
Hiermee wordt aangegeven of u aanmelden met Hallo `azure login` opdracht of het importeren van publicatie-instellingen, uw CLI-profiel en de logboeken worden opgeslagen in een `.azure` directory zich in uw `user` directory. Uw `user` map wordt beveiligd door het besturingssysteem. We raden u echter aan dat u rekening houden met extra stappen tooencrypt uw `user` directory. U kunt dit doen in de volgende manieren Hallo:

* Hallo directory eigenschappen wijzigen van Windows, of gebruik van BitLocker.
* Schakel op de Mac, FileVault voor Hallo-directory.
* Op Ubuntu, Hallo versleutelde Home directory functie te gebruiken. Andere Linux-distributies bieden vergelijkbare functies.

## <a name="logging-out"></a>Afmelden
toolog uit gebruik Hallo volgende opdracht:

    azure logout -u <username>

Als Hallo abonnementen die zijn gekoppeld aan worden Hallo account alleen met Active Directory, logboekregistratie verwijderingen Hallo abonnement informatie uit het lokale profiel Hallo geverifieerde. Echter, als een bestand met publicatie-instellingen ook voor Hallo abonnementen is geïmporteerd, afmelden alleen verwijderingen Active Directory gegevens uit het lokale profiel Hallo gerelateerde.

## <a name="next-steps"></a>Volgende stappen
* toouse Azure CLI-opdrachten, Zie [Azure CLI-opdrachten in de modus Resource Manager](virtual-machines/azure-cli-arm-commands.md) en [Azure CLI-opdrachten in de modus van de Service Management](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn meer informatie over hello Azure CLI broncode downloaden, problemen, rapport of bijdragen toohello project, gaat u naar Hallo [GitHub-opslagplaats voor hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Als u met hello Azure CLI of Azure problemen, gaat u naar Hallo [Azure-Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
