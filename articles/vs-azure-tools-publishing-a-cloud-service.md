---
title: een Cloudservice met behulp van hulpprogramma's van Azure Hallo aaaPublishing | Microsoft Docs
description: Meer informatie over hoe Azure toopublish serviceprojecten cloud met behulp van Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Een Cloudservice met hello Azure-hulpprogramma's publiceren
U kunt uw Azure-toepassing rechtstreeks vanuit Visual Studio publiceren met hello Azure-hulpprogramma's voor Microsoft Visual Studio. Visual Studio ondersteunt geïntegreerd tooeither publiceren Hallo fasering of Hallo productie-omgeving van een cloudservice.

Voordat u een Azure-toepassing publiceren kunt, moet u een Azure-abonnement hebben. U moet ook een cloud service- en storage-account toobe-gebruikt door uw toepassing instellen. U kunt deze instellen op Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!IMPORTANT]
> Wanneer u publiceert, kunt u de implementatieomgeving Hallo voor uw cloudservice. Ook moet u een opslagaccount dat gebruikte toostore Hallo toepassingspakket voor implementatie. Hallo-toepassingspakket wordt na de implementatie van Hallo storage-account verwijderd.
> 
> 

Wanneer u ontwikkelen en testen van een Azure-toepassing, kunt u Web Deploy toopublish wijzigingen stapsgewijs voor uw web-rollen. Nadat u uw toepassing tooa-implementatieomgeving publiceert, Web Deploy Hiermee kunt u de wijzigingen direct toohello virtuele machine waarop wordt Hallo Webrol implementeren. U geen toopackage en uw volledige Azure-toepassing telkens wanneer die u uw web-functie tootest om Hallo wijzigingen tooupdate wilt publiceren. U kunt uw web-rol wijzigingen beschikbaar in de cloud voor het testen van uw toepassing gepubliceerde tooa implementatieomgeving zonder te wachten toohave Hallo hebben met deze methode.

Gebruik uw Azure-toepassing en een Webrol tooupdate hello toopublish procedures te volgen met behulp van Web Deploy:

* Publiceren of een Azure-toepassing vanuit Visual Studio-pakket
* Een Webrol als onderdeel van het Hallo-ontwikkeling en tests cyclus bijwerken

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Publiceren of een Azure-toepassing vanuit Visual Studio-pakket
Wanneer u uw Azure-toepassing publiceert, kunt u een van de taken te volgen Hallo kunt doen:

* Een servicepakket maken: U kunt dit pakket en Hallo service configuration file toopublish uw toepassing tooa implementatieomgeving van Hallo [klassieke Azure-Portal](http://go.microsoft.com/fwlink/?LinkID=213885).
* Publiceren van uw Azure-project vanuit Visual Studio: toopublish uw toepassing rechtstreeks tooAzure, gebruik Hallo Wizard publiceren. Zie voor informatie [Publish Azure Application Wizard](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate servicepakket vanuit Visual Studio
1. Wanneer u bent klaar toopublish wordt uw toepassing Solution Explorer, open Hallo snelmenu voor hello Azure-project met uw rollen te openen en kies publiceren.
2. toocreate servicepakket alleen, als volgt:  
   
   1. In het snelmenu Hallo voor hello Azure project, kies **pakket**.
   2. In Hallo **pakket Azure toepassing** in het dialoogvenster een pakket Hallo serviceconfiguratie waarvoor u toocreate wilt kiezen en kies vervolgens Hallo build-configuratie.
   3. (optioneel) tooturn over extern bureaublad voor cloudservice Hallo nadat u het publiceert, selecteer Hallo **extern bureaublad inschakelen voor alle rollen** selectievakje en selecteer vervolgens **instellingen** tooconfigure extern bureaublad. Als u toodebug uw cloudservice wilt nadat u deze hebt gepubliceerd, schakelt u foutopsporing op afstand door te selecteren **externe foutopsporing inschakelen voor alle rollen**.
      
      Zie voor meer informatie [met behulp van extern bureaublad met de Azure-rollen](vs-azure-tools-remote-desktop-roles.md).
   4. toocreate Hallo van het pakket, kiest u Hallo **pakket** koppeling.
      
      Verkenner toont de bestandslocatie Hallo Hallo nieuw pakket gemaakt. U kunt deze locatie kopiëren zodat u kunt het gebruiken van Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
   5. toopublish dit pakket tooa implementatieomgeving, moet u deze locatie zoals pakketlocatie Hallo wanneer u een cloudservice maken en implementeren van deze omgeving pakket tooan Hello [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
3. (Optioneel) toocancel Hallo het implementatieproces op Hallo snelmenu voor Hallo regelitem in Hallo activiteitenlogboek, kies **annuleren en verwijder**. Dit Hallo implementatieproces stopt en verwijdert deze Hallo implementatieomgeving van Azure.
   
   > [!NOTE]
   > tooremove deze implementatieomgeving nadat deze is geïmplementeerd, moet u Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
   > 
   > 
4. (Optioneel) Nadat uw rolinstanties hebt gestart, Visual Studio Hallo implementatieomgeving automatisch weergegeven in Hallo **Cloudservices** knooppunt in Server Explorer. Hier kunt kunt u Hallo status Hallo afzonderlijke rolinstanties zien. Zie [het beheer van Azure-resources met Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md).hello volgende afbeelding ziet u Hallo rolinstanties als ze nog steeds in Hallo status Bezig met initialiseren:
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Een Webrol als onderdeel van Hallo ontwikkeling en tests cyclus bijwerken
Als uw app back-end-infrastructuur stabiel is, maar Hallo webrollen moeten vaker worden bijgewerkt, kunt u Web Deploy tooupdate alleen een Webrol in uw project. Dit is handig wanneer u niet wilt toorebuild en opnieuw implementeren Hallo back-end-werkrollen, of als er meerdere webrollen en gewenste tooupdate slechts één Hallo webrollen.

### <a name="requirements"></a>Vereisten
Hier volgen de Webrol Hallo vereisten toouse Web Deploy tooupdate:

* **Voor het ontwikkelen en testen van uitsluitend:** Hallo wijzigingen zijn aangebracht rechtstreeks toohello virtuele machine waarop de Webrol hello wordt uitgevoerd. Als deze virtuele machine toobe gerecycled heeft, is Hallo wijzigingen gaan verloren omdat Hallo oorspronkelijke pakket die u hebt gepubliceerd gebruikte toorecreate Hallo virtuele machine voor Hallo-rol. U moet uw toepassing tooget Hallo meest recente wijzigingen voor de Webrol Hallo opnieuw publiceren.
* **Alleen webrollen kunnen worden bijgewerkt:** werkrollen kunnen niet worden bijgewerkt. U kunt bovendien Hallo RoleEntryPoint in web role.cs niet bijwerken.
* **Biedt slechts ondersteuning voor één exemplaar van een Webrol:** kunt u meerdere exemplaren van een Webrol hebben in uw implementatieomgeving. Meerdere webrollen elke met slechts één exemplaar worden echter ondersteund.
* **U moet verbindingen met extern bureaublad inschakelen:** dit is vereist zodat Web Deploy Hallo gebruiker en wachtwoord tooconnect toohello virtuele machine toodeploy Hallo wijzigingen toohello server met Internet Information Services (IIS) kunt gebruiken. Bovendien moet u mogelijk tooconnect toohello virtuele machine tooadd een tooIIS vertrouwd certificaat op deze virtuele machine. (Dit zorgt ervoor dat de verbinding met extern Hallo voor IIS die wordt gebruikt door Web Deploy beveiligd is.)

Hallo volgende procedure wordt ervan uitgegaan dat u van Hallo gebruikmaakt **Publish Azure Application** wizard.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable implementeren wanneer u publiceren van uw webtoepassing
1. Hallo tooenable **inschakelen Web Deploy** voor alle web-rollen selectievakje inschakelt, moet u eerst Extern bureaublad-verbindingen configureren. Selecteer **extern bureaublad inschakelen** voor alle functies en vervolgens levering Hallo referenties die gebruikt tooconnect op afstand in Hallo worden **configuratie voor extern bureaublad** vak dat wordt weergegeven. Zie [met behulp van extern bureaublad met de Azure-rollen](vs-azure-tools-remote-desktop-roles.md) voor meer informatie.
2. Web Deploy tooenable voor alle web-rollen in uw toepassing hello schakelt **Web Deploy inschakelen voor alle webrollen**.
   
    Een gele driehoek van de waarschuwing wordt weergegeven. Web Deploy gebruikt een niet-vertrouwd, zelf-ondertekend certificaat standaard niet aanbevolen wordt voor het uploaden van gevoelige gegevens. Als u dit proces toosecure voor gevoelige gegevens moet, kunt u een SSL-certificaat toobe gebruikt voor verbindingen Web Deploy kunt toevoegen. Dit certificaat moet toobe een vertrouwd certificaat. Voor informatie over het toodo, Zie de sectie Hallo **tooMake Web implementeren Secure** verderop in dit onderwerp.
3. Kies **volgende** tooshow hello **samenvatting** scherm en kies vervolgens **publiceren** toodeploy Hallo-cloudservice.
   
    Hallo-cloudservice is gepubliceerd. Hallo virtuele machine die wordt gemaakt heeft externe verbindingen zijn ingeschakeld voor IIS zodat Web Deploy gebruikte tooupdate kunnen worden uw web-rollen zonder deze opnieuw te publiceren.
   
   > [!NOTE]
   > Als u meer dan één exemplaar is geconfigureerd voor een Webrol hebt, wordt een waarschuwing weergegeven, waarin staat dat elke Webrol worden beperkt tooone exemplaar alleen in het Hallo-pakket dat toopublish uw toepassing heeft gemaakt. Selecteer **OK** toocontinue. Zoals vermeld in de sectie vereisten hello, kunt u meer dan één Webrol, maar slechts één exemplaar van elke rol hebben.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate uw Webrol door het gebruik van Web Deploy
1. Web Deploy, toouse wijzigingen toohello CodeProject voor een van uw web-rollen maken in Visual Studio dat u toopublish wilt, en met de rechtermuisknop op dit projectknooppunt in uw oplossing en wijst u te**publiceren**. Hallo **webpublicatie** dialoogvenster wordt weergegeven.
2. (Optioneel) Als u een vertrouwde toouse van SSL-certificaat voor externe verbindingen voor IIS hebt toegevoegd, kunt u het selectievakje Hallo **toestaan niet-vertrouwd certificaat** selectievakje. Zie voor informatie over hoe tooadd een certificaat toomake Web Deploy beveiligen Hallo sectie **tooMake Web implementeren beveiligde** verderop in dit onderwerp.
3. toouse Web Deploy, Hallo publiceren mechanisme moet Hallo-gebruikersnaam en wachtwoord dat u zich ingesteld voor verbinding met extern bureaublad wanneer u Hallo-pakket voor het eerst hebt gepubliceerd.
   
   1. In **gebruikersnaam**, Voer Hallo-gebruikersnaam.
   2. In **wachtwoord**, Hallo wachtwoord invoeren.
   3. (Optioneel) Als u dit wachtwoord in dit profiel toosave wilt, kies **wachtwoord opslaan**.
4. toopublish hello wijzigingen tooyour Webrol, kies **publiceren**.
   
    Hallo statusregel geeft **publiceren gestart**. Wanneer Hallo publiceren is voltooid, **publiceren is voltooid** wordt weergegeven. Hallo wijzigingen zijn nu de Webrol geïmplementeerde toohello op de virtuele machine. U kunt nu uw Azure-toepassing in hello Azure-omgeving tootest uw wijzigingen.

### <a name="toomake-web-deploy-secure"></a>Web implementeren Secure tooMake
1. Web Deploy gebruikt een niet-vertrouwd, zelf-ondertekend certificaat standaard niet aanbevolen wordt voor het uploaden van gevoelige gegevens. Als u dit proces toosecure voor gevoelige gegevens moet, kunt u een SSL-certificaat toobe gebruikt voor verbindingen Web Deploy kunt toevoegen. Dit certificaat moet toobe een vertrouwd certificaat, die u van een certificeringsinstantie (CA ontvangt).
   
    toomake Web Deploy beveiligde voor elke virtuele machine voor elk van uw web-rollen, moet u Hallo vertrouwd certificaat dat u toouse voor toohello van web deploy uploaden [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885). Dit zorgt ervoor dat certificaat Hallo toohello virtuele machine die wordt gemaakt voor de Webrol Hallo wanneer u uw toepassing publiceren wordt toegevoegd.
2. een vertrouwde tooIIS toouse van een SSL-certificaat voor externe verbindingen tooadd als volgt te werk:
   
   1. tooconnect toohello virtuele machine die wordt uitgevoerd Hallo Webrol, selecteer Hallo exemplaar van de Webrol Hallo in **Cloud Explorer** of **Server Explorer**, en kies vervolgens Hallo **verbinding maken via Extern bureaublad** opdracht. Voor gedetailleerde stappen voor het tooconnect toohello virtuele machine, Zie [met behulp van extern bureaublad met de Azure-rollen](vs-azure-tools-remote-desktop-roles.md).
      
      Uw browser wordt u gevraagd toodownload een. RDP-bestand.
   2. tooadd een SSL-certificaat open Hallo management-service in IIS-beheer. SSL in IIS-beheer inschakelen door het openen van Hallo **bindingen** koppeling in Hallo **actie** deelvenster. Hallo **sitebinding toevoegen** dialoogvenster wordt weergegeven. Kies **toevoegen**, en kies vervolgens HTTPS in Hallo **Type** vervolgkeuzelijst. In Hallo **SSL-certificaat** Kies Hallo SSL-certificaat dat u heeft ondertekend door een CA en dat u hebt geüpload toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885). Zie voor meer informatie [verbindingsinstellingen voor Hallo Management-Service configureren](http://go.microsoft.com/fwlink/?LinkId=215824).
      
      > [!NOTE]
      > Als u een vertrouwd certificaat voor SSL toevoegt, geel Hallo waarschuwing driehoek niet langer weergegeven bij Hallo **Wizard publiceren**.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Bestanden in Hallo servicepakket opnemen
Mogelijk moet u specifieke bestanden tooinclude in het servicepakket zodat ze beschikbaar zijn op Hallo virtuele machine die is gemaakt voor een rol. Bijvoorbeeld, kunt u tooadd een .exe- of een MSI-bestand dat wordt gebruikt door een script voor opstarten tooyour servicepakket. Of u moet mogelijk tooadd een assembly die een rol of de werknemer webrolproject vereist. tooinclude-bestanden die moeten echter toegevoegd toohello oplossing voor uw Azure-toepassing.

### <a name="tooinclude-files-in-hello-service-package"></a>bestanden in het servicepakket Hallo tooinclude
1. een servicepakket assembly tooa tooadd gebruik Hallo stappen te volgen:
   
   1. In **Solution Explorer** open Hallo projectknooppunt voor Hallo-project dat assembly Hallo waarnaar wordt verwezen ontbreekt.
   2. tooadd hello assembly toohello project, open Hallo snelmenu voor Hallo **verwijzingen** map en kies vervolgens **verwijzing toevoegen**. Hallo verwijzing toevoegen dialoogvenster wordt weergegeven.
   3. Kies Hallo referentie dat u wilt dat tooadd en kies vervolgens Hallo **OK** knop.
      
      verwijzing naar een Hallo toegevoegd toohello lijst onder Hallo **verwijzingen** map.
   4. Open het snelmenu Hallo voor Hallo-assembly die u hebt toegevoegd en kies **eigenschappen**. Hallo **eigenschappen** venster wordt weergegeven.
      
      tooinclude deze assembly in Hallo service pakket in Hallo **lokale kopie lijst** kiezen **True**.
2. In **Solution Explorer** open Hallo projectknooppunt voor Hallo-project dat assembly Hallo waarnaar wordt verwezen ontbreekt.
3. tooadd hello assembly toohello project, open Hallo snelmenu voor Hallo **verwijzingen** map en kies vervolgens **verwijzing toevoegen**. Hallo **verwijzing toevoegen** dialoogvenster wordt weergegeven.
4. Kies Hallo referentie dat u wilt dat tooadd en kies vervolgens Hallo **OK** knop.
   
    verwijzing naar een Hallo toegevoegd toohello lijst onder Hallo **verwijzingen** map.
5. Open het snelmenu Hallo voor Hallo-assembly die u hebt toegevoegd en kies **eigenschappen**. Hallo eigenschappenvenster wordt weergegeven.
6. tooinclude deze assembly in Hallo service pakket in Hallo **lokale kopie** Kies **True**.
7. tooinclude-bestanden in het servicepakket Hallo die zijn toegevoegd aan de rol-webproject met tooyour Hallo snelmenu voor het Hallo-bestand openen en kies vervolgens **eigenschappen**. Van Hallo **eigenschappen** venster kiezen **inhoud** van Hallo **Build Action** keuzelijst met invoervak.
8. tooinclude-bestanden in het servicepakket Hallo die zijn toegevoegd aan de tooyour werkrolproject, Hallo snelmenu voor het Hallo-bestand openen en kies vervolgens **eigenschappen**. Van Hallo **eigenschappen** venster kiezen **kopiëren indien nieuwer** van Hallo **kopie toooutput directory** keuzelijst met invoervak.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over publiceren tooAzure vanuit Visual Studio, Zie [Publish Azure Application Wizard](vs-azure-tools-publish-azure-application-wizard.md).

