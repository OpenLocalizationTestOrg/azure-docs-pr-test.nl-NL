---
title: aaaDeploy SAP S/4HANA of BW/4HANA op een virtuele machine in Azure | Microsoft Docs
description: SAP S/4HANA of BW/4HANA op een virtuele machine in Azure implementeren
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>SAP S/4HANA of BW/4HANA in Azure implementeren
Dit artikel wordt beschreven hoe toodeploy S/4HANA in Azure met behulp van Hallo SAP toestel Cloudbibliotheek (SAP CAL) 3.0. toodeploy andere SAP HANA-oplossingen, zoals BW/4HANA Hallo Volg dezelfde stappen.

> [!NOTE]
Ga voor meer informatie over Hallo SAP CAL toohello [SAP-Cloudbibliotheek toestel](https://cal.sap.com/) website. SAP heeft ook een blog over Hallo [SAP Cloud toestel bibliotheek 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Zoals van 29 mei 2017, kunt u hello Azure Resource Manager-implementatiemodel bovendien toohello minder voorkeur klassieke implementatie toodeploy Hallo SAP CAL model. Het is raadzaam om nieuwe Resource Manager-implementatiemodel hello te gebruiken en het klassieke implementatiemodel Hallo negeren.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Stapsgewijs toodeploy Hallo oplossing

Hallo volgende schermafbeeldingen reeks ziet u hoe toodeploy S/4HANA in Azure met behulp van SAP CAL Hallo. Hallo-proces werkt Hallo dezelfde manier voor andere oplossingen, zoals BW/4HANA.

Hallo **oplossingen** pagina bevat een aantal Hallo SAP CAL HANA gebaseerde oplossingen beschikbaar in Azure. **SAP S 4HANA 1610 FPS01, Fully-Activated toestel** bevindt zich in het middelste rij Hallo:

![SAP CAL oplossingen](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Een account maken in Hallo SAP CAL
1. toosign in toohello SAP CAL voor Hallo eerste keer gebruikt uw SAP-gebruiker of een andere gebruiker die is geregistreerd bij SAP. Definieer een SAP CAL-account dat wordt gebruikt door Hallo SAP CAL toodeploy apparaten op Azure. In de definitie van Hallo-account moet u:

    a. Hallo-implementatiemodel in Azure (Resource Manager of klassiek) selecteren.

    b. Voer uw Azure-abonnement. Een SAP CAL-account kan alleen tooone abonnement worden toegewezen. Als u meer dan één abonnement nodig hebt, moet u toocreate een ander SAP CAL-account.

    c. Hallo SAP CAL machtiging toodeploy geven in uw Azure-abonnement.

    > [!NOTE]
    Hallo volgende stappen laten zien hoe toocreate een SAP CAL-account voor implementaties van Resource Manager. Als u al een SAP CAL-account dat gekoppelde toohello klassieke implementatiemodel, hebt u *moet* toofollow deze toocreate stappen een nieuwe SAP CAL-account. Hallo nieuwe SAP CAL-account moet toodeploy in Hallo Resource Manager-model.

2. Maak een nieuwe SAP CAL-account. Hallo **Accounts** pagina ziet u drie opties voor Azure: 

    a. **Microsoft Azure (klassiek)** Hallo klassieke implementatiemodel is en niet langer voorkeur.

    b. **Microsoft Azure** Hallo nieuwe Resource Manager-implementatiemodel is.

    c. **Windows Azure worden beheerd door 21Vianet** is een optie in China die gebruikmaakt van het klassieke implementatiemodel Hallo.

    toodeploy in Hallo Resource Manager-model, selecteer **Microsoft Azure**.

    ![Details van SAP CAL-Account](./media/cal-s4h/s4h-pic-2a.png)

3. Voer hello Azure **abonnements-ID** die u kunt vinden op Hallo Azure-portal.

   ![SAP CAL Accounts](./media/cal-s4h/s4h-pic3c.png)

4. tooauthorize hello SAP CAL toodeploy in hello Azure-abonnement dat u hebt gedefinieerd, klikt u op **autoriseren**. Hallo na pagina wordt weergegeven in Hallo browsertabblad:

   ![Internet Explorer cloud services-aanmeldingspagina](./media/cal-s4h/s4h-pic4c.png)

5. Als meer dan één gebruiker wordt weergegeven, kies Hallo Microsoft-account dat is gekoppeld toobe Hallo CO-beheerder van hello Azure-abonnement u hebt geselecteerd. Hallo na pagina wordt weergegeven in Hallo browsertabblad:

   ![Bevestiging van Internet Explorer cloud-services](./media/cal-s4h/s4h-pic5a.png)

6. Klik op **accepteren**. Als het Hallo-autorisatie is geslaagd, wordt Hallo SAP CAL-account definitie opnieuw wordt weergegeven. Na korte tijd, wordt een bericht bevestigd Hallo autorisatieproces is geslaagd.

7. nieuw gemaakte SAP CAL-account tooyour gebruiker tooassign hello, Voer uw **gebruikers-ID** in Hallo tekstvak op Hallo rechts en klik op **toevoegen**.

   ![Accountkoppeling toouser](./media/cal-s4h/s4h-pic8a.png)

8. Klik op tooassociate uw account met Hallo gebruiker dat u toosign in toohello SAP-CAL **revisie**. 
 
9. toocreate hello koppeling tussen uw gebruikers- en Hallo nieuw gemaakte SAP CAL-account, klikt u op **maken**.

   ![Koppeling van gebruiker tooSAP CAL-account](./media/cal-s4h/s4h-pic9b.png)

Een SAP CAL-account dat kan worden gemaakt:

- Gebruik Hallo Resource Manager-implementatiemodel.
- SAP-systemen implementeren in uw Azure-abonnement.

U kunt nu toodeploy S/4HANA starten in uw gebruikerabonnement in Azure.

> [!NOTE]
Voordat u doorgaat, moet u bepalen of er Azure core quota's voor virtuele machines van Azure H-serie. Hallo-momenteel Hallo SAP CAL toodeploy H-serie virtuele machines van Azure gebruikt enkele van Hallo SAP HANA-oplossingen. Uw Azure-abonnement mogelijk geen quota's core H-serie voor H-serie. Als dit het geval is, moet u mogelijk toocontact ondersteuning van Azure tooget een quotum van ten minste 16 kernen van H-serie.

> [!NOTE]
Wanneer u een oplossing op Azure in Hallo SAP CAL implementeert, kan het gebeuren dat u slechts één Azure-regio kunt. toodeploy in Azure-regio's dan Hallo een voorgesteld door Hallo SAP CAL, moet u een abonnement CAL uit SAP toopurchase. Ook moet u mogelijk een bericht met SAP toohave tooopen uw toodeliver CAL-account is ingeschakeld in Azure-regio's dan Hallo die in eerste instantie voorgesteld.

### <a name="deploy-a-solution"></a>Een oplossing implementeren

We implementeren van een oplossing van Hallo **oplossingen** pagina Hallo SAP CAL. Hallo SAP CAL heeft twee reeksen toodeploy:

- Een eenvoudige reeks die gebruikmaakt van één pagina toodefine Hallo system toobe geïmplementeerd
- Een geavanceerde reeks waarmee u bepaalde keuzes op VM-grootten 

Hallo basic pad toodeployment Hier ziet.

1. Op Hallo **accountdetails** pagina, moet u:

    a. Een SAP CAL-account selecteren. (Gebruik een account dat is gekoppeld toodeploy met Resource Manager-implementatiemodel Hallo.)

    b. Geef het exemplaar van een **naam**.

    c. Selecteer een Azure **regio**. Hallo SAP CAL stelt voor een regio. Als u een andere Azure-regio moet en u een SAP CAL-abonnement hebt, moet u een licentie voor clienttoegang tooorder abonnement met SAP.

    d. Voer een model **wachtwoord** voor Hallo-oplossing van acht of negen tekens. Hallo-wachtwoord wordt gebruikt voor beheerders van de verschillende onderdelen Hallo Hallo.

   ![SAP CAL-standaardmodus: Exemplaar maken](./media/cal-s4h/s4h-pic10a.png)

2. Klik op **maken**, en in Hallo-bericht dat wordt weergegeven, klikt u op **OK**.

   ![SAP CAL ondersteund VM-grootten](./media/cal-s4h/s4h-pic10b.png)

3. In Hallo **persoonlijke sleutel** in het dialoogvenster, klikt u op **Store** toostore Hallo persoonlijke sleutel in Hallo SAP CAL. wachtwoordbeveiliging toouse voor de persoonlijke sleutel hello, klikt u op **downloaden**. 

   ![SAP CAL persoonlijke sleutel](./media/cal-s4h/s4h-pic10c.png)

4. Lees Hallo SAP CAL **waarschuwing** bericht en op **OK**.

   ![SAP CAL waarschuwing](./media/cal-s4h/s4h-pic10d.png)

    Hallo-implementatie wordt nu uitgevoerd. Na enige tijd, afhankelijk van Hallo omvang en complexiteit van Hallo-oplossing (Hallo SAP CAL een schatting biedt), Hallo status wordt weergegeven als active en klaar voor gebruik.

5. toofind hello virtuele machines die zijn verzameld met andere gekoppelde resources in één resourcegroep hello, gaat u toohello Azure-portal: 

   ![SAP CAL-objecten die zijn geïmplementeerd in de nieuwe portal Hallo](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. Op Hallo SAP CAL portal Hallo status wordt weergegeven als **Active**. tooconnect toohello oplossing, klikt u op **Connect**. Verschillende opties tooconnect toohello verschillende onderdelen worden geïmplementeerd in deze oplossing.

   ![SAP CAL exemplaren](./media/cal-s4h/active_solution.png)

7. Voordat u een van de Hallo opties tooconnect toohello geïmplementeerd systemen gebruiken kunt, klikt u op **Getting Started Guide**. 

   ![Verbinding maken met toohello exemplaar](./media/cal-s4h/connect_to_solution.png)

    Hallo documentatie namen Hallo gebruikers voor elk van Hallo connectiviteit methoden. Hallo-wachtwoorden voor die gebruikers toohello master wachtwoord die u hebt gedefinieerd bij Hallo begin van het implementatieproces Hallo ingesteld. In de documentatie Hallo andere meer functionaliteit gebruikers worden weergegeven met hun wachtwoorden, kunt u toosign in toohello system geïmplementeerd. 

    Bijvoorbeeld, als u Hallo SAP-GUI die vooraf geïnstalleerd op de extern bureaublad van Windows-machine hello, Hallo S/4 systeem als volgt uitzien:

   ![SM50 in Hallo SAP-GUI vooraf geïnstalleerd](./media/cal-s4h/gui_sm50.png)

    Of als u Hallo DBACockpit, Hallo-exemplaar als volgt uitzien:

   ![SM50 in Hallo DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

Binnen een paar uur wordt een gezonde SAP S/4 toestel geïmplementeerd in Azure.

Als u een SAP CAL-abonnement hebt gekocht, ondersteund SAP implementaties via Hallo SAP CAL volledig in Azure. Hallo Ondersteuningswachtrij is BC-VCM-CAL.







