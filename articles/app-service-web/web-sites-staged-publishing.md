---
title: aaaSet up faseringsomgevingen voor web-apps in Azure App Service | Microsoft Docs
description: Meer informatie over hoe toouse gefaseerde publiceren voor web-apps in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Faseringsomgevingen in Azure App Service instellen
<a name="Overview"></a>

Wanneer u implementeert uw web-app, web-app op Linux-, mobiele back-end- en API-app te[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), u kunt afzonderlijke implementatiesleuf tooa in plaats van Hallo standaard productiesite implementeren bij uitvoering in Hallo **standaard**of **Premium** modus van App Service-plan. Implementatiesites zijn daadwerkelijk live apps met hun eigen hostnamen. App-inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van Hallo productiesite. Implementatie van de implementatiesleuf van uw toepassing tooa heeft Hallo volgende voordelen:

* U kunt appwijzigingen in een gefaseerde installatie implementatiesleuf valideren voordat het wisselen met Hallo productiesite.
* Een app tooa sleuf eerst implementeren en deze in productie wisselen zorgt u ervoor dat alle exemplaren van Hallo sleuf voordat gewisseld naar de productie zijn opgewarmd. Hierdoor is er uitvaltijd wanneer u uw app implementeert. Hallo verkeer omleiden naadloze is en er zijn geen aanvragen worden verwijderd als gevolg van de wisseling bewerkingen. Deze volledige werkstroom kan worden geautomatiseerd door configureren [automatisch wisselen](#Auto-Swap) wanneer vooraf swap-validatie is niet nodig.
* Als een wisseling heeft Hallo sleuf met eerder voorbereide app Hallo vorige productie-app. Als gewisseld naar de productiesite Hallo Hallo-wijzigingen zijn niet zoals u verwacht, kunt u dezelfde wisselen onmiddellijk back-tooget uw "laatst bekende goede site" hello uitvoeren.

Elke App Service plan modus ondersteunt een verschillend aantal implementatiesites. toofind hello aantal sleuven van uw app-modus ondersteunt, Zie [prijzen van App Service](https://azure.microsoft.com/pricing/details/app-service/).

* Wanneer uw app meerdere sleuven heeft, kunt u het Hallo-modus niet wijzigen.
* Schalen is niet beschikbaar voor niet-productieve sleuven.
* Gekoppelde bronbeheer wordt niet ondersteund voor niet-productieve sleuven. In Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) u kunt dit mogelijk invloed op een productiesite alleen voorkomen door het Hallo niet productiesite tooa App Service plan modus tijdelijk te verplaatsen. Opmerking die niet-productieve Hallo sleuf moet Hallo nogmaals delen dezelfde modus met Hallo productiesite voordat u kunt twee Hallo sleuven omwisselen.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Een implementatiesleuf toevoegen
Hallo-app moet worden uitgevoerd in Hallo **standaard** of **Premium** modus in volgorde voor u tooenable meerdere implementatiesites.

1. In Hallo [Azure Portal](https://portal.azure.com/), opent u uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Kies Hallo **implementatiesites** optie en klik vervolgens op **sleuf toevoegen**.
   
    ![Voeg een nieuwe implementatiesleuf][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Als Hallo app nog niet Hallo **standaard** of **Premium** modus, ontvangt u een bericht weergegeven dat aangeeft Hallo ondersteund modi voor het inschakelen van voorbereide publiceren. Op dit moment hebt u Hallo optie tooselect **Upgrade** en navigeer toohello **Scale** tabblad van uw app voordat u doorgaat.
   > 
   > 
3. In Hallo **toevoegen van een sleuf** blade Hallo sleuf een naam geven en selecteer of tooclone app configuratie uit een andere bestaande implementatiesleuf. Klik op Hallo vinkje toocontinue.
   
    ![Configuratiebron][ConfigurationSource1]
   
    Hallo eerste keer dat u een site toevoegen wordt alleen hebt u twee mogelijkheden: configuratie van de kloon uit Hallo standaard sleuf in productie of helemaal niet.
    Wanneer u meerdere sleuven hebt gemaakt, kunt u zich kunt tooclone configuratie uit een sleuf dan Hallo in productie:
   
    ![Configuratie van bronnen][MultipleConfigurationSources]
4. Klik in de resourceblade van de app, op **implementatiesites**, klikt u vervolgens op een implementatiesleuf tooopen die sleuf resource-blade met een set van metrische gegevens en configuratie net als elke andere app. Hallo naam van Hallo sleuf weergegeven bovenaan Hallo Hallo blade tooremind u die u bekijkt implementatiesleuf Hallo.
   
    ![Implementatiesleuf titel][StagingTitle]
5. Klik op Hallo app-URL in de blade Hallo-sleuf. Kennisgeving Hallo implementatiesleuf heeft een eigen hostnaam en is ook een live-app. toolimit openbare toegang toohello implementatiesleuf Zie [App Service Web-App – blok web access toonon productie-implementatiesites](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

Er is geen inhoud nadat de implementatiesleuf is gemaakt. U kunt toohello sleuf vanaf een andere opslagplaats vertakking of een geheel andere opslagplaats implementeren. U kunt ook Hallo siteconfiguratie wijzigen. Gebruik Hallo publiceren of de implementatie-referenties die zijn gekoppeld aan de implementatiesleuf Hallo voor updates van inhoud.  U kunt bijvoorbeeld [toothis sleuf met git publiceren](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Configuratie voor implementatiesites
Als u een configuratie uit een andere implementatiesleuf kloon is Hallo gekloonde configuratie kan worden bewerkt. Bovendien volgen sommige configuratie-elementen Hallo inhoud via een wisseling (kan niet in sleuf worden specifieke) terwijl andere configuratie-elementen blijft in Hallo dezelfde sleuf na een wisseling (sleuf specifieke). Hallo ziet volgende lijsten Hallo-configuratie die wordt gewijzigd wanneer u sleuven wisselen.

**Instellingen die worden omgewisseld**:

* Algemene instellingen - zoals framework-versie, 64-32-bits, Web-sockets
* App-instellingen (kan worden geconfigureerd toostick tooa sleuf)
* Verbindingsreeksen (kan worden geconfigureerd toostick tooa sleuf)
* Handlertoewijzingen
* Instellingen voor controle en diagnose
* WebJobs-inhoud

**Instellingen die niet worden omgewisseld**:

* Publicatie-eindpunten
* Aangepaste domeinnamen
* SSL-certificaten en bindingen
* Schaalinstellingen
* WebJobs planners

een instelling of verbinding tekenreeks toostick tooa appsite (geen verwisseld) toegang Hallo tooconfigure **toepassingsinstellingen** blade voor een specifieke site en vervolgens selecteert Hallo **sleuf instelling** in voor Hallo configuratie-elementen die Hallo sleuf moeten houden. Houd er rekening mee dat een configuratie-element als gemarkeerd sleuf specifieke heeft Hallo effect van het tot stand brengen van dat element als niet verwisselbare over alle Hallo implementatiesites Hallo app gekoppeld.

![Sleufinstellingen][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Wisselen implementatiesites 
U kunt wisselen implementatiesites in Hallo **overzicht** of **implementatiesites** weergave van de resource-blade van uw app.

> [!IMPORTANT]
> Voordat u een app van een implementatiesleuf naar de productie wisselen, zorg ervoor dat alle niet-specifieke sleufinstellingen precies zoals u wilt dat toohave zijn geconfigureerd in Hallo wisselen doel.
> 
> 

1. tooswap implementatiesites, klikt u op Hallo **wisselen** knop in de opdrachtbalk Hallo van Hallo app of in de opdrachtbalk Hallo van een implementatiesleuf.
   
    ![Knop wisselen][SwapButtonBar]

2. Zorg ervoor dat Hallo wisselen bron- en wisselen doel correct zijn ingesteld. Hallo wisselen doel is meestal Hallo productiesite. Klik op **OK** toocomplete Hallo-bewerking. Wanneer het Hallo-bewerking is voltooid, hebt Hallo implementatiesites zijn gewisseld.

    ![Wisseling voltooien](./media/web-sites-staged-publishing/SwapImmediately.png)

    Voor Hallo **wisseling met voorbeeld** type wisselen, Zie [wisseling met voorbeeld (meerdere fase swap)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Wisselen met voorbeeld (meerdere fase swap)

Wisselen met voorbeeld of meerdere stap wisseling, validatie van de site-specifieke configuratie-elementen, zoals verbindingsreeksen vereenvoudigen.
Bedrijfskritieke werkbelastingen gewenste toovalidate die Hallo app werkt zoals verwacht tijdens het Hallo-productiesite van configuratie is toegepast en moet u deze validatie uitvoeren *voordat* Hallo-app wordt gewisseld naar de productie. Wisseling met voorbeeld is wat u nodig hebt.

> [!NOTE]
> Wisseling met voorbeeld wordt niet ondersteund in web-apps op Linux.

Wanneer u Hallo gebruikt **wisselen met voorbeeld** optie (Zie [implementatiesites wisselen](#Swap)), App Service Hallo te volgen:

- Houdt Hallo bestemming sleuf ongewijzigd zodat bestaande werkbelasting op die sleuf (bijvoorbeeld productie) wordt niet beïnvloed.
- Van toepassing hello configuratie-elementen van Hallo sleuf toohello bron doelsleuf, met inbegrip van Hallo sleuf-specifieke verbindingsreeksen en app-instellingen.
- Hallo werkprocessen op Hallo bron sleuf met behulp van deze elementen van de hiervoor genoemde configuratie opnieuw is opgestart.
- Wanneer u Hallo wisseling voltooien: verplaatst Hallo pre-warmed-up bronsite in Hallo doelsleuf. Hallo doelsleuf verplaatst naar het Hallo-bronsite als een handmatige wisseling in.
- Wanneer u annuleert Hallo wisselen: Hallo-configuratie-elementen van Hallo bron sleuf toohello bron sleuf past.

U kunt een voorbeeld precies hoe Hallo-app met Hallo bestemming sleuf configuratie wordt uitgevoerd. Nadat de validatie is voltooid, kunt u Hallo wisseling in een aparte stap voltooien. Deze stap is Hallo bijkomend voordeel dat Hallo bron sleuf al met de gewenste configuratie Hallo opgewarmd en clients niet geen downtime ondervinden wordt.  

Voorbeelden voor hello Azure PowerShell-cmdlets voor meerdere stap wisseling zijn opgenomen in hello Azure PowerShell-cmdlets voor implementatie sleuven sectie.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Automatisch wisselen configureren
Uw app met nul koude start en uitvaltijd implementeren automatisch wisselen zodat DevOps-scenario's waar u toocontinuously wilt voor end-klanten van Hallo-app. Wanneer een implementatiesleuf is geconfigureerd voor automatisch wisselen naar de productie, elke keer dat u uw code update toothat sleuf pushen, wordt App Service automatisch Hallo app wisselen naar de productie nadat deze al is opgewarmd in sleuf Hallo.

> [!IMPORTANT]
> Wanneer u automatisch wisselen voor een site inschakelt, zorg ervoor dat siteconfiguratie Hallo exact Hallo configuratie is bedoeld voor Hallo doel sleuf (meestal Hallo productiesite).
> 
> 

> [!NOTE]
> Automatisch wisselen wordt niet ondersteund in web-apps op Linux.

Automatisch wisselen configureren voor een sleuf is eenvoudig. Volg onderstaande stappen voor Hallo:

1. In **Implementatiesites**, selecteert u een niet-productiesite en kiest u **toepassingsinstellingen** in die sleuf resource-blade.  
   
    ![][Autoswap1]
2. Selecteer **op** voor **automatisch wisselen**, selecteer Hallo gewenste doel sleuf in **automatisch wisselen sleuf**, en klik op **opslaan** in de opdrachtbalk Hallo. Zorg ervoor dat de configuratie voor Hallo sleuf exact Hallo configuratie is bedoeld voor Hallo doel sleuf.
   
    Hallo **meldingen** tabblad knippert een groene **geslaagd** zodra het Hallo-bewerking is voltooid.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest automatisch wisselen voor uw app, kunt u eerst een niet-productieve doel sleuf in selecteren **automatisch wisselen sleuf** toobecome bekend bent met het Hallo-functie.  
   > 
   > 
3. Een implementatiesleuf code push toothat uitvoeren. Automatisch wisselen gebeurt na een korte periode en Hallo update, worden weergegeven op de doel-sleuf URL.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback een productie-app na wisselen
Als er fouten worden geïdentificeerd in het nadat een wisseling sleuf, rollover van Hallo sleuven back tootheir vooraf wisselen statussen door Hallo dezelfde twee sleuven onmiddellijk wisselen.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Aangepaste opgewarmd voordat wisselen
Sommige apps mogelijk aangepaste opgewarmd acties. Hallo `applicationInitialization` configuratie-element in web.config-bestand kunt u toospecify aangepaste initialisatie met acties toobe uitgevoerd voordat een aanvraag wordt ontvangen. het wisselen van Hallo wacht tot deze toocomplete aangepaste opgewarmd. Hier volgt een voorbeeld web.config fragment.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete een implementatiesleuf
Hallo-blade voor een implementatiesleuf, open Hallo implementatiesleuf blade, klikt u op **overzicht** (Hallo standaardpagina) en klik op **verwijderen** in de opdrachtbalk Hallo.  

![Een Implementatiesleuf verwijderen][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Azure PowerShell-cmdlets voor implementatiesites
Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell, inclusief ondersteuning voor het beheren van implementatiesites in Azure App Service biedt.

* Zie voor informatie over het installeren en configureren van Azure PowerShell, en Azure PowerShell verifiëren met uw Azure-abonnement, [hoe tooinstall en configureren van Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Een webtoepassing maken
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Een implementatiesleuf te maken
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Initieert een wisseling met revisie (meerdere fase swap) en doelsleuf sleuf configuratie toosource toepassen
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Annuleren van een wisseling in behandeling (swap met revisie) en bron siteconfiguratie herstellen
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Wisselen implementatiesites
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Implementatiesite verwijderen
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Azure Command-Line Interface (Azure CLI)-opdrachten voor Implementatiesites
Hello Azure CLI biedt platformoverschrijdende-opdrachten voor het werken met Azure, met inbegrip van ondersteuning voor het beheren van App Service-implementatiesites.

* Voor instructies over het installeren en configureren van hello Azure CLI, inclusief informatie over het tooconnect Azure CLI tooyour Azure-abonnement, Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).
* toolist hello opdrachten die beschikbaar zijn voor Azure App Service in hello Azure CLI aanroepen `azure site -h`.

> [!NOTE] 
> Voor [Azure CLI 2.0](https://github.com/Azure/azure-cli) -opdrachten voor implementatiesites, Zie [az appservice web implementatiesleuf](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>sitelijst voor Azure
Bel voor informatie over apps in het huidige abonnement Hallo Hallo **azure sitelijst**, Hallo voorbeeld te volgen.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>Azure site maken
aanroepen van een implementatiesleuf toocreate **azure site maken** en geeft Hallo-naam van een bestaande app en het Hallo-naam van Hallo sleuf toocreate, zoals in het volgende voorbeeld Hallo.

`azure site create webappslotstest --slot staging`

tooenable broncodebeheer voor Hallo nieuwe sleuf gebruik Hallo **--git** optie, zoals in het volgende voorbeeld Hallo.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>Azure site wisselen
toomake Hallo bijgewerkte implementatiesleuf Hallo productie-app, gebruikt u Hallo **azure site wisselen** opdracht tooperform een wisselbewerking wordt uitgevoerd, zoals in het volgende voorbeeld Hallo. Hallo productie-app wordt niet uitvaltijd ondervinden, noch wordt een koude start ondergaan.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>Azure site verwijderen
toodelete een implementatiesleuf die niet langer nodig is, gebruik Hallo **azure site verwijderen** opdracht, zoals in het volgende voorbeeld Hallo.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Bekijk een web-app in werking. [App Service uitproberen](https://azure.microsoft.com/try/app-service/) onmiddellijk en maak een tijdelijke app: geen creditcard nodig en zonder verdere verplichtingen.
> 
> 

## <a name="next-steps"></a>Volgende stappen
[Azure App Service-Web App – blokkeren web access toonon productie implementatiesites](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[inleiding tooApp-Service op Linux](./app-service-linux-intro.md)
[gratis proefversie van Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

