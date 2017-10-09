---
title: een installatiekopie van de virtuele machine in Azure Marketplace Hallo aaaManaging | Microsoft Docs
description: "Gedetailleerde richtlijnen voor hoe toomanage uw virtuele machine een installatiekopie in Azure Marketplace Hallo na de initiële publicatie"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Na productie-handleiding voor de virtuele machine biedt in hello Azure Marketplace
Dit artikel wordt uitgelegd hoe u een aanbieding live virtuele machine in Azure Marketplace Hallo kunt bijwerken. Dit leidt u door het Hallo-proces voor het toevoegen van een of meer nieuwe SKU's tooan bestaande aanbieding. Ook leidt u door het Hallo-proces voor het verwijderen van een aanbieding voor live virtuele machine of de SKU van Hallo Marketplace.

Nadat een aanbieding/SKU tijdelijk worden opgeslagen in Hallo [Azure-portal](http://portal.azure.com), kunt u Hallo volgende tekstvakken niet wijzigen:

* **ID bieden**: Ga In de Hallo-portal publiceren te**virtuele machines** en selecteer uw aanbieding. Klik vervolgens op **VM-INSTALLATIEKOPIEËN** > **bieden id**.
* **SKU-id**: Ga In de Hallo-portal publiceren te**virtuele machines** en selecteer uw aanbieding. Klik vervolgens op **SKU's** > **toevoegen van een SKU**.
* **Publisher Namespace**: Ga In de Hallo-portal publiceren te**virtuele machines** > **scenario** > **Vertel ons over uw bedrijf** (te vinden onder 'Stap 2 registreren van uw bedrijf') > **Publisher Namespace** > **Namespace**.

Nadat het Hallo aanbieding/SKU wordt vermeld in Hallo [Marketplace](http://azure.microsoft.com/marketplace), kunt u Hallo volgende tekstvakken niet wijzigen:

* **ID bieden**: Ga In de Hallo-portal publiceren te**virtuele machines** en selecteer uw aanbieding. Klik vervolgens op **VM-INSTALLATIEKOPIEËN** > **bieden id**.
* **SKU-id**: Ga In de Hallo-portal publiceren te**virtuele machines** en selecteer uw aanbieding. Klik vervolgens op **SKU's** > **toevoegen van een SKU**.
* **Publisher Namespace**: Ga In de Hallo-portal publiceren te**virtuele machines** > **scenario** > **Vertel ons over uw bedrijf** (te vinden onder "Stap 2 registreren") **Publisher Namespace** > **Namespace**.
* **Poorten**: Ga In de Hallo-portal publiceren te**virtuele machines** en selecteer uw aanbieding. Klik vervolgens op **VM-INSTALLATIEKOPIEËN** > **poorten openen**.
* **Wijziging van de vermelde SKU(s) prijzen**
* **Facturering model wijziging van de vermelde SKU(s)**
* **Verwijderen van de gebieden van de vermelde SKU(s) facturering**
* **Veranderende Hallo gegevens telling van de vermelde SKU(s) schijf**

## <a name="update-hello-technical-details-of-a-sku"></a>Technische details van een SKU Hallo bijwerken
een nieuwe versie toohello tooadd SKU vermeld en uw aanbieding publiceren, als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **VM-INSTALLATIEKOPIEËN** tabblad.
4. In Hallo **SKU's** sectie, zoek Hallo SKU die u tooupdate wilt.
5. Toevoegen van een nieuwe versienummer van Hallo SKU, en klik op Hallo  **+**  knop. de nieuwe versie Hallo moet zich in een indeling X.Y.Z, waarbij X, Y en Z gehele getallen zijn. Wijzigingen in versie moet alleen incrementele.
6. In Hallo **OS VHD URL** vak, Voer Hallo shared access signature voor URI voor het besturingssysteem Hallo VHD gemaakt en Hallo wijzigingen opslaan.

   > [!IMPORTANT]
   > U kan geen incrementele/verlagen Hallo aantal gegevensschijven van een vermelde SKU. Moet u in dit geval toocreate een nieuwe SKU. Raadpleeg voor gedetailleerde richtlijnen toohello sectie [toevoegen van een nieuwe SKU onder een vermelde aanbieding](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![VM-installatiekopieën](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>Niet-technische details van een aanbieding of een SKU Hallo bijwerken
U kunt niet-technische hello (marketing, juridische, ondersteuning, categorieën) bijwerken details van uw live aanbieding of SKU in Hallo Marketplace.

### <a name="update-hello-offer-description-and-logos"></a>Beschrijving van de aanbieding Hallo en logo's bijwerken
tooupdate Hallo details van de aanbieding en uw aanbieding publiceren, als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **MARKETING** tabblad.
4. Klik op **Engels (V.S.)**.
5. Klik op Hallo **DETAILS** tabblad. In Hallo **beschrijving** sectie, update Hallo aanbieding **titel**, **samenvatting**, en **LONG SUMMARY** en Hallo wijzigingen op te slaan.

   > [!NOTE]
   > Wanneer u Hallo SKU details bijwerkt, worden op de hoogte van deze beperkingen: 
   * Geef geen dubbele tekst voor de beschrijving van de aanbieding Hallo en Hallo SKU beschrijving.
   * Geef geen dubbele tekst voor Hallo SKU titel en Hallo aanbieding lange samenvatting. 
   * Geef geen dubbele tekst voor Hallo SKU titel en Hallo aanbodoverzicht.
   >
   >

    ![Details](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. In Hallo **logo's** sectie Hallo **DETAILS** tabblad, Hallo logo's bijwerken. Zorg ervoor dat Hallo logo's, Hallo volgen [richtlijnen voor Azure Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > Een pictogram hero is optioneel. U kunt een pictogram hero niet tooupload. Nadat een pictogram hero is geüpload, is er echter geen toodelete inrichten op Hallo portal publiceren. Ga als volgt Hallo [hero pictogram richtlijnen](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![Logo 's](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Hallo SKU beschrijving van update
tooupdate hello SKU gegevens en uw aanbieding publiceren als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **MARKETING** tabblad.
4. Klik op **Engels (V.S.)**.
5. Klik op Hallo **plannen** tabblad. In Hallo **SKU's** sectie, het bijwerken van Hallo SKU **titel**, **samenvatting**, en **beschrijving** en Hallo wijzigingen op te slaan.

   > [!NOTE]
   > Wanneer u Hallo SKU details bijwerkt, worden op de hoogte van deze beperkingen: 
   * Geef geen dubbele tekst voor de beschrijving van de aanbieding Hallo en Hallo SKU beschrijving. 
   * Geef geen dubbele tekst voor Hallo SKU titel en Hallo aanbieding lange samenvatting. 
   * Geef geen dubbele tekst voor Hallo SKU titel en Hallo aanbodoverzicht.
   >
   >
6. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![Abonnementen](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Bestaande koppelingen wijzigen of toevoegen van nieuwe koppelingen
bestaande koppelingen toochange of toevoegen van nieuwe koppelingen en vervolgens opnieuw uw aanbieding publiceren, als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **MARKETING** tabblad.
4. Klik op **Engels (V.S.)**.
5. Klik op Hallo **koppelingen** tabblad.
6. een nieuwe koppeling, in Hallo tooadd **koppelingen** sectie, klikt u op **+ koppeling toevoegen**. In Hallo **koppeling toevoegen** dialoogvenster Voer Hallo koppeling **titel** en **URL** en Hallo wijzigingen op te slaan. U kunt een koppeling met informatie waarmee klanten invoeren.
7. tooupdate of verwijder een bestaande koppeling Hallo koppeling selecteren en klik op Hallo **bewerken** knop of Hallo **verwijderen** knop.

   > [!NOTE]
   > Zorg ervoor dat Hallo koppelingen die u hebt ingevoerd in deze sectie naar behoren werken omdat deze koppelingen ophalen gevalideerd tijdens uw productie-aanvraagproces.
   >
   >
8. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![Koppelingen](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Koppeling toevoegen](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Een bestaande installatiekopie van het voorbeeld wijzigen of toevoegen van een nieuwe installatiekopie van het voorbeeld
een bestaande voorbeeld toochange installatiekopie installatiekopieën van het nieuwe voorbeeld toevoegen en vervolgens opnieuw uw aanbieding publiceren, als volgt te werk:

> [!NOTE]
> Slechts één voorbeeld van afbeelding wordt weergegeven in Hallo [Azure-portal](https://portal.azure.com).
>
>

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **MARKETING** tabblad.
4. Klik op **Engels (V.S.)**.
5. Klik op Hallo **voorbeeld INSTALLATIEKOPIEËN** tabblad.
6. een nieuwe installatiekopie van het voorbeeld in Hallo tooadd **voorbeeld installatiekopieën** sectie, klikt u op **nieuwe INSTALLATIEKOPIE uploaden** en sla de wijzigingen Hallo.

   > [!NOTE]
   > Inclusief de installatiekopie van een voorbeeld is optioneel.
   >
7. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![Installatiekopieën van het voorbeeld](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Hallo juridische inhoud bijwerken
tooupdate Hallo juridische inhoud en uw aanbieding publiceren, als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **MARKETING** tabblad.
4. Klik op **Engels (V.S.)**.
5. Klik op Hallo **juridische** tabblad. In Hallo **juridische** sectie, het bijwerken van uw beleid/gebruiksvoorwaarden. Plak Hallo beleidsregels/voorwaarden in Hallo **gebruiksvoorwaarden** vak en Hallo wijzigingen opslaan.
6. Hallo tekenlimiet voor Hallo juridische gebruiksvoorwaarden is 1 miljoen tekens.
7. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![Juridische informatie](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Bijwerken van informatie over het Hallo-ondersteuning
tooupdate hello ondersteuningsinformatie en uw aanbieding publiceren, als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **ondersteuning** tabblad.
4. In Hallo **Engineering, neem contact op met** sectie update Hallo engineering contactgegevens. Deze gegevens worden alleen voor interne communicatie tussen Hallo partner en Microsoft gebruikt.
5. In Hallo **Customer Support** sectie, bijwerken Hallo ondersteuning contact op met de details en Hallo **ONDERSTEUNEN URL**. Deze gegevens worden alleen voor interne communicatie tussen Hallo partner en Microsoft gebruikt.

   > [!NOTE]
   > Als u wilt dat alleen e-mailondersteuning tooprovide, voert u een dummy-telefoonnummer in Hallo **Customer Support** sectie. In dit geval is Hallo e-mail die u hebt opgegeven in plaats daarvan gebruikt.
   >
   >
6. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![Ondersteuning](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Hallo categorieën bijwerken
tooupdate hello categorieën sectie voor uw aanbieding en uw aanbieding publiceren als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **categorieën** tabblad.
4. In Hallo **categorieën** sectie, het bijwerken van Hallo categorieën voor uw aanbieding en het Hallo wijzigingen opslaan. U kunt toofive categorieën voor hello Azure Marketplace-galerie.
5. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
6. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![Categorieën](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Voeg een nieuwe SKU onder een vermelde aanbieding
een nieuwe SKU van uw live aanbod tooadd als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **SKU's** tabblad. Klik vervolgens op **toevoegen van een SKU**. 
4. Voer in het dialoogvenster hello, een **SKU-id** in kleine letters. Selecteer Hallo **brengt uw eigen factureringsmodel license (BYOL)** selectievakje in als u wilt dat toopublish Hallo nieuwe SKU met een facturering BYOL-model. Schakel het selectievakje Hallo anders uit. Klik op Hallo maatstreepjes markeren toocreate een nieuwe SKU. Als u niet Hallo BYOL factureringsmodel, Hallo factureringsmodel toohourly automatisch ingesteld. Als u Hallo 30 dagen gratis proefversie voor Hallo per uur facturering model wilt, selecteer **één maand** voor **Is een gratis proefversie beschikbaar?** Selecteer anders **Nee proefversie**. (**Is een gratis proefversie beschikbaar?**  wordt alleen weergegeven als u geen BYOL hebt geselecteerd tijdens het maken van nieuwe SKU Hallo.)

   > [!IMPORTANT]
   > **De SKU van Hallo Marketplace verbergen omdat moet altijd worden aangekocht via een oplossingssjabloon** moet **Ja** *alleen* als u bent goedgekeurd voor het publiceren van een oplossingssjabloon. Anders wordt deze optie altijd moet **Nee**.
   >
   >
4. Hallo-menu op Hallo links en klik op Hallo **VM-INSTALLATIEKOPIEËN** tabblad en uitzoeken Hallo nieuwe SKU die u hebt gemaakt.
5. tooset maximaal Hallo nieuwe SKU, Zie [behalen van certificaten voor uw VM-installatiekopie](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) voor hulp.
6. tooadd marketingmateriaal voor nieuwe SKU Hallo, Zie [bieden Marketplace marketing inhoud](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. Prijsinformatie voor tooadd Hallo nieuwe SKU, Zie [instellen van uw prijzen](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

    ![SKU 's](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Toevoegen van een SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Hallo aantal gegevensschijven voor een lijst SKU wijzigen
U kan geen incrementele/verlagen Hallo aantal gegevensschijven van een vermelde SKU. Moet u in dit geval toocreate een nieuwe SKU. Raadpleeg voor gedetailleerde richtlijnen toohello sectie [toevoegen van een nieuwe SKU onder een vermelde aanbieding](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Een vermelde aanbieding verwijderen uit Hallo Marketplace
Verschillende aspecten moeten toobe afgehandeld in geval van een aanvraag tooremove een live aanbieding Hallo. tooget richtlijnen van Hallo support team tooremove een vermelde aanbieding van Hallo Marketplace, als volgt te werk:

1. Een ondersteuningsticket op Hallo verhogen [een incident maken](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) pagina.

2. Selecteer **probleemtype** als **aanbiedingen beheren**, en selecteer **categorie** als **al een aanbieding en/of SKU wijzigen in productie**.
3. Hallo-aanvraag indienen.

Hallo-ondersteuningsteam begeleidt u bij verwijdering van Hallo aanbieding/SKU.

> [!NOTE]
> U kunt altijd Hallo aanbieding verwijderen terwijl het de status concept (maar niet fasering of productie). Op Hallo **geschiedenis** tabblad **concept verwijderen**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Een vermelde SKU van Hallo Marketplace verwijderen
toodelete een vermelde SKU van Hallo Marketplace, als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).

2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Klik in deelvenster Hallo op Hallo links op Hallo **SKU's** tabblad.
4. Selecteer Hallo SKU toodelete wilt en klikt u op Hallo **verwijderen** knop.
5. Ga toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish Hallo aanbieding in Hallo Marketplace.
6. Nadat het Hallo aanbieding is gepubliceerd in Hallo Marketplace, wordt Hallo SKU verwijderd uit Hallo Marketplace en hello Azure-portal.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Huidige versie van een vermelde SKU Hallo verwijderen uit Hallo Marketplace
toodelete hello huidige versie van een vermelde SKU van Hallo Marketplace, als volgt te werk: 

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).

2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **VM-INSTALLATIEKOPIEËN** tabblad.
4. Selecteer Hallo SKU waarvan de huidige versie die u wilt toodelete en klikt u op Hallo **verwijderen** knop.
5. Ga toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish Hallo aanbieding in Hallo Marketplace.
6. Nadat het Hallo-aanbieding wordt opnieuw gepubliceerd in Hallo Marketplace, Hallo huidige versie van Hallo vermelde SKU uit Hallo Marketplace en hello Azure-portal is verwijderd. Hallo SKU vervolgens teruggedraaid tooits vorige versie.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Hallo aanbieding prijs tooproduction waarden herstellen
toorevert hello aanbieding prijs tooproduction waarden als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).
2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **prijzen** tabblad.
4. Selecteer een regio waarvan u wilt dat prijzen tooreset.

    ![Prijzen van regio 's](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Voor SKU's met een uur facturering model reset Hallo prijzen voor alle Hallo kernen ze in productie voor de geselecteerde regio Hallo zijn. Zorg voor SKU's met een factureringsmodel BYOL SKU die beschikbaar zijn in de regio Hallo HALLO hallo selectievakje inschakelt voor Hallo SKU in Hallo **EXTERNALLY-LICENSED (BYOL) SKU beschikbaarheid** sectie.

    ![Prijsmodellen](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Klik op **AUTOPRICE andere markten op basis van de prijzen IN de Verenigde Staten**.

   > [!NOTE]
   > Hallo knoplabel kan afwijken, afhankelijk van het Hallo-regio die u selecteert. Omdat we Verenigde Staten hebt geselecteerd, Hallo knop heet **AUTOPRICE andere markten gebaseerd op prijzen IN de Verenigde Staten**.
   >
   >

    ![Autoprice](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. Op pagina 1 van Hallo Autoprice wizard, kies Hallo base markt en klikt u op Hallo **pijl** knop.

    ![Base markt](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. Op pagina 2, service-abonnementen en meters (kernen) kiezen en op Hallo **pijl** knop.

    ![Service-abonnementen en meters](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. Klik op de pagina 3 **wisselknop alle** tooselect alle regio's. Ook kunt u de selectievakjes voor specifieke regio's handmatig selecteren. Klik op Hallo **pijl** knop.

    ![Kies markten](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. Op pagina 4 bekijkt hello wisselkoersen en op **voltooien**. Hallo wizard stelt Hallo volgens tooyour selecties prijzen.

11. Op Hallo **prijzen** tabblad **weergave Samenvatting en wijzigingen**.
    Voor **versie weergeven**, selecteer **concept**, en voor **vergelijken met**, selecteer **productie**. Als er geen verschil prijscategorie, hersteld Hallo prijzen toohello productiewaarden is.

    ![Samenvatting weergeven en wijzigingen](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
13. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Hallo facturering model tooproduction waarden herstellen
toorevert hello facturering model tooproduction waarden als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).

2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **SKU's** tabblad.
4. Klik op Hallo **bewerken** knop toorevert Hallo facturering model. Hallo-venster dat wordt geopend, schakel of Hallo **facturering en licenties extern van Azure (aka Bring Your Own License) wordt uitgevoerd** selectievakje.

    ![Facturering bewerken](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Stappen Hallo in 'Revert Hallo prijs tooproduction waarden aanbieding' in dit artikel.
6. Ga toohello **publiceren** tabblad en klik op **PUSH tooSTAGING**. Zie voor gedetailleerde instructies over het testen van uw aanbieding in Hallo staging-omgeving [testen van uw VM-aanbieding voor Hallo Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Nadat u uw aanbieding hebt getest in fasering, gaat u toohello **publiceren** tabblad in Hallo portal publiceren. Klik op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Hallo zichtbaarheidsinstelling van een waarde van de vermelde SKU toohello productie te herstellen
toorevert hello zichtbaarheidsinstelling van een vermelde SKU toohello waarde van de productie, als volgt te werk:

1. Meld u aan toohello [portal publiceren](https://publish.windowsazure.com).

2. Ga toohello **virtuele machines** tabblad, en selecteer uw aanbieding.
3. Hallo-menu op Hallo links en klik op Hallo **SKU's** tabblad.
4. Selecteer uw SKU en Hallo zichtbaarheidsinstelling Hallo waarde van de SKU toohello productie te herstellen.

    ![Zichtbaarheid](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Nadat u met Hallo wijzigingen bent klaar, klikt u op **goedkeuring aanvragen tooPUSH tooPRODUCTION** toorepublish uw aanbieding in Hallo Marketplace.

## <a name="see-also"></a>Zie ook
* [Aan de slag: Publiceren een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md)
* [Toekenning reporting begrijpen](marketplace-publishing-report-payout.md)
* [Uw wederverkoper Cloud Solution Provider stimulans wijzigen](marketplace-publishing-csp-incentive.md)
* [Algemene problemen publishing in Hallo Marketplace](marketplace-publishing-support-common-issues.md)
* [Ondersteuning krijgen als een publisher](marketplace-publishing-get-publisher-support.md)
* [Maak een VM-installatiekopie lokale](marketplace-publishing-vm-image-creation-on-premise.md)
* [Maak een virtuele machine met Windows in hello Azure preview-portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
