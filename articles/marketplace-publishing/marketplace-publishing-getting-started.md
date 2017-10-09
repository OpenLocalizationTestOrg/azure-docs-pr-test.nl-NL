---
title: aaaOverview van hoe toocreate en implementeren van een aanbieding toohello Marketplace | Microsoft Docs
description: Hallo stappen vereist toobecome een goedgekeurde Microsoft developer begrijpen en maken en implementeren van een installatiekopie van virtuele machine, sjabloon, data-service of developer-service in hello Azure Marketplace
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>Publiceren en beheren van een aanbieding in hello Azure Marketplace
In dit artikel krijgt u toohelp ontwikkelaars maken, implementeren en beheren van hun oplossingen die worden vermeld in hello Azure Marketplace voor andere Azure-klanten en partners toopurchase en gebruiken.

## <a name="marketplace-publishing"></a>Publicatie van de Marketplace
Als een Azure publisher, u kunt distribueren en verkopen van uw oplossing innovatieve of service tooother ontwikkelaars, onafhankelijke softwareleveranciers, en IT-professionals in Hallo Marketplace. Via Hallo Marketplace, u kunt bereiken klanten die tooquickly willen hun cloud-gebaseerde toepassingen en mobiele oplossingen ontwikkelen. Als uw oplossing is bedoeld voor zakelijke gebruikers, kunt u tooconsider hello [AppSource](http://appsource.microsoft.com) marketplace.


## <a name="supported-types-of-solutions"></a>Ondersteunde typen oplossingen
Hallo eerste wat u wilt toodo zoals een uitgever is toodefine wat voor soort oplossing aangeboden door uw bedrijf. Hallo Marketplace ondersteunt Hallo typen aanbiedingen te volgen:

|Oplossingstype|Virtuele machine|Oplossingssjabloon|
|---|---|---|
|**Definitie**|Vooraf geconfigureerde afbeeldingen met een volledig geïnstalleerde besturingssysteem en een of meer toepassingen. De installatiekopie van een virtuele machine biedt Hallo informatie nodig toocreate en implementeren van virtuele machines in Azure Virtual Machines service Hallo.|Een gegevensstructuur die kunt verwijzen naar een of meer verschillende Azure-services, waaronder services gepubliceerd door andere verkopers. Azure-abonnees kunnen worden gebruikt toodeploy aanbiedingen voor een of meer op een enkele, gecoördineerde wijze.|
|**Voorbeeld**|U hebt gemaakt en gevalideerd van een virtuele machine met een databaseservice innovatieve als een Azure publisher. Andere Azure-abonnees wilt tooprocure en implementeren van deze virtuele machine in hun cloud service-omgevingen.|Als een Azure publisher, hebt u een set services van gebundeld in Azure om het snel toodeploy cloudservices met taakverdeling, verbeterde beveiliging en hoge beschikbaarheid. Andere Azure-abonnees kunnen tijd besparen door Hallo oplossingssjabloon die voldoet aan hun doel te kopen. Ze geen toomanually vinden, schaft u, implementeren en configureren Hallo dezelfde of gelijksoortige Azure-services.|

> [!NOTE]
> Een aantal stappen worden gedeeld tussen verschillende soorten oplossingen Hallo en andere unieke toohello respectieve type oplossing zijn. In dit artikel bevat een kort overzicht van stappen Hallo hoeft u toocomplete voor elk type oplossing.

## <a name="publish-a-solution"></a>Publiceren van een oplossing
![Benoemen, registreren, publiceren](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>Uw oplossing benoemen voor voorafgaande goedkeuring
een virtuele machine toopublish [oplossing](https://createopportunity.azurewebsites.net) toohello voltooid Hallo gecertificeerd voor Microsoft Azure Marketplace **oplossing benoeming formulier**.

>[!NOTE]
> Als u met een Partner-accountmanager of een Partner DX Manager werkt, vraagt u ze toonominate uw oplossing voor hello Azure gecertificeerd programma. U kunt ook gaan toohello [Microsoft Azure-gecertificeerd](http://createopportunity.azurewebsites.net) webpagina's en vul Hallo aanvraagformulier. Voer Hallo e-mailadres van uw Partner-accountmanager of DX Partner Manager in Hallo **Sponsor contact op met Microsoft** vak.

Als u voldoen aan Hallo in aanmerking komt criteria in Hallo [Azure Marketplace deelname beleid](http://go.microsoft.com/fwlink/?LinkID=526833) en uw aanvraag wordt goedgekeurd, wordt aan de slag met tooonboard u uw oplossing toohello Marketplace.

### <a name="register-your-account-as-a-microsoft-seller"></a>Uw account registreren als een Microsoft-verkoper
Registreren van uw Microsoft-account als een [Microsoft Developer-account](marketplace-publishing-accounts-creation-registration.md).

### <a name="publish-your-solution"></a>Publiceren van uw oplossing
toopublish een oplossing toohello Marketplace, als volgt te werk:
1. Hallo niet-technische vereisten voldoen.

    a. Hallo voldoen [niet-technische vereisten](marketplace-publishing-pre-requisites.md).

    b. Hallo voldoen [VM technische vereisten](marketplace-publishing-vm-image-creation-prerequisites.md).

    c. Hallo voldoen [technische vereisten voor oplossing](marketplace-publishing-solution-template-creation-prerequisites.md).

2. Maak uw aanbieding.

    a. Maak een [virtuele machine](marketplace-publishing-vm-image-creation.md) bieden.

    b. Maak een [oplossingssjabloon](marketplace-publishing-solution-template-creation.md) bieden.

3. Maken van uw aanbieding [inhoud marketing](marketplace-publishing-push-to-staging.md).

4. Test uw aanbieding in fasering.

    a. Testen van uw VM-aanbieding in [fasering](marketplace-publishing-vm-image-test-in-staging.md).

    b. Testen van uw oplossing sjabloon aanbieding in [fasering](marketplace-publishing-solution-template-test-in-staging.md).

5. Implementeer uw aanbieding toohello [Marketplace](marketplace-publishing-push-to-production.md).


### <a name="create-and-manage-a-virtual-machine-image"></a>Maken en beheren van de installatiekopie van een virtuele machine
Maken en beheren van een installatiekopie van een virtuele machine met behulp van deze bronnen:
* Maak een VM-installatiekopie [lokale](marketplace-publishing-vm-image-creation-on-premise.md).
* Maken van een virtuele machine met [Windows in hello Azure-portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Maken van een virtuele machine met [Linux in hello Azure-portal](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Algemene problemen aangetroffen tijdens [VHD maken](marketplace-publishing-vm-image-creation-troubleshooting.md).

## <a name="manage-your-solution"></a>Beheren van uw oplossing
Uw oplossing met behulp van Hallo volgende resources beheren:
* [Lees Hallo na productie-handleiding voor de virtuele machine biedt](marketplace-publishing-vm-image-post-publishing.md)
* [Niet-technische details van een aanbieding of een SKU Hallo bijwerken](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [Technische details van een aanbieding of een SKU Hallo bijwerken](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [Voeg een nieuwe SKU onder een vermelde aanbieding](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [Hallo aantal gegevensschijven voor een lijst SKU wijzigen](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [Een vermelde aanbieding verwijderen uit Hallo Marketplace](marketplace-publishing-vm-image-post-publishing.md)
* [Een vermelde SKU van Hallo Marketplace verwijderen](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [Huidige versie van een vermelde SKU Hallo verwijderen uit Hallo Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [Hallo aanbieding prijs tooproduction waarden herstellen](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [Hallo facturering model tooproduction waarden herstellen](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [Hallo zichtbaarheidsinstelling van een waarde van de vermelde SKU toohello productie te herstellen](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [Uw wederverkoper Cloud Solution Provider stimulans wijzigen](marketplace-publishing-csp-incentive.md)
* [Inzicht in uw toekenning rapportage](marketplace-publishing-report-payout.md)
* [Ondersteuning krijgen als een publisher](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>Aanvullende bronnen
[Instellen van Azure PowerShell](marketplace-publishing-powershell-setup.md)
