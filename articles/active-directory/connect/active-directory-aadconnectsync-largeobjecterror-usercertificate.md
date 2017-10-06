---
title: 'Azure AD Connect-synchronisatie: LargeObject afhandeling van fouten als gevolg van userCertificate-kenmerk | Microsoft Docs'
description: In dit onderwerp biedt herstelstappen aan Hallo voor LargeObject fouten worden veroorzaakt door userCertificate-kenmerk.
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Azure AD Connect-synchronisatie: LargeObject afhandeling van fouten als gevolg van userCertificate-kenmerk

Azure AD dwingt een maximumlimiet van **15** waarden op Hallo van het certificaat **userCertificate** kenmerk. Als Azure AD Connect een object met meer dan 15 waarden tooAzure AD exporteert, Azure AD geeft een **LargeObject** fout opgetreden bij het bericht:

>*'Hallo ingerichte object is te groot. Trim Hallo aantal kenmerkwaarden voor dit object. Hallo bewerking uit te voeren in Hallo volgende synchronisatiecyclus..."*

Hallo LargeObject fout kan worden veroorzaakt door een andere AD-kenmerken. tooconfirm inderdaad wordt veroorzaakt door Hallo userCertificate kenmerk, moet u tooverify tegen Hallo object zich in de on-premises AD dat of in Hallo [Synchronization Service Manager Metaverse zoeken](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

tooobtain hello lijst van objecten in uw tenant met LargeObject fouten, een van de volgende methoden hello gebruiken:

 * Als uw tenant wordt ingeschakeld voor Azure AD Connect Health voor synchroniseren, raadpleegt u toohello [synchronisatie foutenrapport](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) opgegeven.
 
 * Hallo e-mailmelding voor directory-synchronisatiefouten dat wordt verzonden aan einde van elke synchronisatiecyclus Hallo heeft Hallo lijst met objecten met fouten LargeObject. 
 * Hallo [Synchronization Service Manager Operations tabblad](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) Hallo lijst met objecten met fouten LargeObject wordt weergegeven als u klikt op Hallo nieuwste tooAzure AD exportbewerking.
 
## <a name="mitigation-options"></a>Risicobeperking opties
Tot Hallo LargeObject fout is opgelost, wordt met andere kenmerk wijzigingen toohello hetzelfde object kan niet worden tooAzure AD geëxporteerd. tooresolve hello fout, kunt u overwegen Hallo volgende opties:

 * Azure AD Connect toobuild 1.1.524.0 upgraden of na. In Azure AD Connect bouwen 1.1.524.0, Hallo out-of-box-synchronisatieregels zijn bijgewerkt toonot export kenmerken userCertificate en userSMIMECertificate als Hallo kenmerken hebben meer dan 15 waarden. Voor meer informatie over het tooupgrade Azure AD Connect verwijzen tooarticle [Azure AD Connect: upgraden van een vorige versie-toohello recente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Implementeer een **uitgaande synchronisatieregel** in Azure AD Connect die exporteert een **null-waarde in plaats van de werkelijke waarden Hallo voor objecten met meer dan 15 certificaat waarden**. Deze optie is geschikt als u geen een Hallo certificaat waarden toobe geëxporteerd tooAzure AD naar objecten met meer dan 15 waarden vereist. Voor meer informatie over het tooimplement deze synchronisatie regel, Raadpleeg de sectie toonext [Implementing sync regel toolimit exporteren van het kenmerk userCertificate](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Verminder het aantal waarden in het certificaat op Hallo Hallo on-premises AD-object (15 of minder) door het verwijderen van de waarden die niet langer in gebruik door uw organisatie. Dit is geschikt als Hallo kenmerk gegevensophoping wordt veroorzaakt door verlopen of niet-gebruikte certificaten. U kunt Hallo [PowerShell-script beschikbaar hier](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) toohelp vinden, back-up maken en verwijderen van verlopen certificaten in uw on-premises AD. Voordat u Hallo certificaten verwijdert, wordt het aanbevolen om te controleren met Hallo infrastructuur van openbare sleutels beheerders in uw organisatie.

 * Configureren van Azure AD Connect tooexclude hello userCertificate kenmerk niet kan worden geëxporteerd tooAzure AD. In het algemeen raadzaam niet deze optie aangezien Hallo-kenmerk kan worden gebruikt door de Microsoft Online Services tooenable specifieke scenario's. In het bijzonder:
    * Hallo userCertificate kenmerk van het gebruikersobject hello wordt gebruikt door de Exchange Online en Outlook-clients voor bericht ondertekening en versleuteling. toolearn meer informatie over deze functie verwijzen tooarticle [S/MIME voor bericht ondertekening en versleuteling](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * Hallo userCertificate kenmerk op Hallo-computerobject wordt gebruikt door Azure AD tooallow Windows 10 lokale domeinapparaten tooconnect tooAzure AD. Raadpleeg tooarticle toolearn meer informatie over deze functie [domeinapparaten tooAzure AD Connect voor Windows 10 optreedt](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Synchronisatie regel toolimit exporteren van het kenmerk userCertificate implementeren
tooresolve hello LargeObject fout wordt veroorzaakt door Hallo userCertificate kenmerk, kunt u een synchronisatieregel voor uitgaande implementeren in Azure AD Connect die exporteert een **null-waarde in plaats van de werkelijke waarden Hallo voor objecten met meer dan 15 certificaat waarden**. Deze sectie beschrijft Hallo stappen vereist tooimplement hello synchronisatieregel voor **gebruiker** objecten. Hallo stappen kunnen worden aangepast voor **Contact** en **Computer** objecten.

> [!IMPORTANT]
> Exporteren van null-waarde Hiermee verwijdert u het certificaat waarden eerder is geëxporteerd tooAzure AD.

Hallo stappen kunnen worden samengevat als:

1. Schakel de sync scheduler en controleer of dat er vindt geen synchronisatie uitgevoerd.
3. Hallo bestaande uitgaande synchronisatieregel voor userCertificate-kenmerk niet vinden.
4. Uitgaande synchronisatieregel Hallo vereist maken.
5. Controleer of nieuwe synchronisatieregel Hallo op een bestaand object met LargeObject fout.
6. Toepassing hello nieuwe synchronisatie regel tooremaining objecten met LargeObject fout.
7. Controleer of er zijn geen onverwachte wijzigingen toobe geëxporteerd tooAzure AD wachten.
8. Hallo wijzigingen tooAzure AD exporteren.
9. Sync scheduler opnieuw in te schakelen.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Step 1. Schakel de sync scheduler uit en controleer of dat er vindt geen synchronisatie uitgevoerd
Zorg ervoor dat er geen synchronisatie plaats terwijl u in het midden bent van de implementatie van een nieuwe synchronisatie Hallo regel tooavoid onbedoelde wijzigingen worden tooAzure AD geëxporteerd. toodisable hello ingebouwde sync scheduler:
1. Start PowerShell-sessie op Hallo Azure AD Connect-server.

2. Geplande synchronisatie uitschakelen door de cmdlet uit te voeren:`Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Hallo zijn voorgaande stappen alleen van toepassing toonewer versies (1.1.xxx.x) van Azure AD Connect met ingebouwde scheduler Hallo. Als u gebruikmaakt van oudere versies (1.0.xxx.x) van Azure AD Connect die gebruikmaakt van Windows Taakplanner of u uw eigen aangepaste scheduler (niet-algemene) tootrigger periodieke synchronisatie gebruikt, moet u toodisable ze dienovereenkomstig.

3. Hallo Start **Synchronization Service Manager** door te gaan tooSTART → Synchronization-Service.

4. Ga toohello **Operations** tabblad en er is geen bewerking met de status bevestigen *'wordt uitgevoerd.'*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>Stap 2. Hallo bestaande uitgaande synchronisatieregel voor het kenmerk userCertificate vinden
Er moet een bestaande synchronisatieregel is ingeschakeld en geconfigureerd tooexport userCertificate kenmerk voor de gebruiker objecten tooAzure AD. Zoek deze synchronisatie regel toofind uit de **voorrang** en **bereik filter** configuratie:

1. Hallo Start **synchronisatie regeleditor** door te gaan tooSTART → synchronisatie Editor regels.

2. Hallo search filters te configureren met Hallo volgende waarden:

    | Kenmerk | Waarde |
    | --- | --- |
    | Richting |**Uitgaand** |
    | MV-objecttype |**Persoon** |
    | Connector |*naam van uw Azure AD-connector* |
    | Connector-objecttype |**gebruiker** |
    | MV-kenmerk |**userCertificate** |

3. Als u OOB (out of box) synchronisatie regels tooAzure AD connector tooexport userCertficiate kenmerk voor gebruikersobjecten gebruikt, ontvangt u Hallo *'Out tooAAD – gebruiker ExchangeOnline'* regel.
4. Noteer Hallo **voorrang** waarde van deze synchronisatieregel.
5. Selecteer Hallo synchronisatieregel en klik op **bewerken**.
6. In Hallo *'Gereserveerde bevestiging regel bewerken'* pop-upvenster, klikt u op **Nee**. (U hoeft niet, we zullen toomake elke regel wijzigen toothis sync).
7. Selecteer in het welkomstscherm bewerken, Hallo **Scoping filter** tabblad.
8. Noteer Hallo filterconfiguratie bereik. Als u Hallo OOB-synchronisatieregel gebruikt, moet exact er **één filter bereikgroep met twee componenten**, waaronder:

    | Kenmerk | Operator | Waarde |
    | --- | --- | --- |
    | Bronobjecttype | GELIJK ZIJN AAN | Gebruiker |
    | cloudMastered | NOTEQUAL | True |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>Stap 3. Uitgaande synchronisatieregel Hallo vereist maken
Hallo nieuwe synchronisatieregel voor moet hebben Hallo dezelfde **bereik filter** en **hogere prioriteit** dan Hallo bestaande synchronisatieregel. Dit zorgt ervoor dat Hallo nieuwe synchronisatieregel van toepassing is toohello dezelfde objecten als de bestaande synchronisatieregel hello en overschrijvingen Hallo bestaande sync-regel voor Hallo userCertificate kenmerk set. toocreate hello synchronisatieregel:
1. In Hallo regeleditor synchronisatie, klikt u op Hallo **nieuwe regel toevoegen** knop.
2. Onder Hallo **tabblad Beschrijving**, bieden Hallo volgende configuratie:

    | Kenmerk | Waarde | Details |
    | --- | --- | --- |
    | Naam | *Geef een naam* | Bijvoorbeeld *'Out tooAAD – aangepaste onderdrukking voor userCertificate'* |
    | Beschrijving | *Geef een beschrijving* | Bijvoorbeeld *"Als userCertificate-kenmerk meer dan 15 waarden heeft, exporteren NULL."* |
    | Verbonden systeem | *Selecteer hello Azure AD-Connector* |
    | Verbonden systeem objecttype | **gebruiker** | |
    | Metaverse-objecttype | **persoon** | |
    | Koppelingstype | **Koppelen** | |
    | Prioriteit | *Kies een getal tussen 1 en 99 liggen* | Hallo getal, gekozen mogen niet worden gebruikt door een bestaande synchronisatieregel en heeft een lagere waarde (en dus hogere prioriteit) dan Hallo bestaande synchronisatieregel. |

3. Ga toohello **Scoping filter** tabblad en gebruik van dezelfde scope Hallo bestaande sync filterregel Hallo implementeren.
4. Overslaan Hallo **Join regels** tabblad.
5. Ga toohello **transformaties** tabblad tooadd een nieuw transformatie met volgende configuratie:

    | Kenmerk | Waarde |
    | --- | --- |
    | Stroomtype |**Expressie** |
    | Doelkenmerk |**userCertificate** |
    | Kenmerk van de gegevensbron |*Gebruik Hallo expressie na*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Klik op Hallo **toevoegen** knop toocreate hello synchronisatieregel.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>Stap 4. Controleer of nieuwe synchronisatieregel Hallo op een bestaand object met LargeObject fout
Dit is tooverify die synchronisatie Hallo regel gemaakt correct werkt op een bestaande AD-object met LargeObject fout voordat u deze toe te tooother objecten passen:
1. Ga toohello **Operations** tabblad in Hallo Synchronization Service Manager.
2. Hallo meest recente tooAzure AD exportbewerking selecteren en klik op een van Hallo-objecten met fouten LargeObject.
3.  Connector ruimte objecteigenschappen pop-welkomstscherm, klik op Hallo **Preview** knop.
4. Selecteer in de Preview pop-welkomstscherm, **volledige synchronisatie** en klik op **doorvoeren Preview**.
5. Sluit welkomstscherm Preview en Connector ruimte objecteigenschappen welkomstscherm.
6. Ga toohello **Connectors** tabblad in Hallo Synchronization Service Manager.
7. Met de rechtermuisknop op Hallo **Azure AD** Connector en selecteer **uitvoeren...**
8. Selecteer in het pop-upmenu Hallo Connector uitvoeren, **exporteren** stap en klik op **OK**.
9. Wacht tot Export tooAzure AD toocomplete en er is geen meer LargeObject-fout voor dit specifieke object bevestigen.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>Stap 5. Hallo nieuwe synchronisatie regel tooremaining objecten met LargeObject fout toepassen
Wanneer de synchronisatieregel Hallo is toegevoegd, moet u toorun de stap van een volledige synchronisatie op Hallo AD-Connector:
1. Ga toohello **Connectors** tabblad in Hallo Synchronization Service Manager.
2. Met de rechtermuisknop op Hallo **AD** Connector en selecteer **uitvoeren...**
3. Selecteer in het pop-upmenu Hallo Connector uitvoeren, **volledige synchronisatie** stap en klik op **OK**.
4. Wachten op Hallo volledige synchronisatie stap toocomplete.
5. Herhaal Hallo bovenstaande stappen voor Hallo resterende AD Connectors hebt u meer dan één AD-Connectors. Meerdere connectors zijn doorgaans vereist als er meerdere on-premises adreslijsten.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>Stap 6. Controleer of er zijn geen onverwachte wijzigingen toobe geëxporteerd tooAzure AD wachten
1. Ga toohello **Connectors** tabblad in Hallo Synchronization Service Manager.
2. Met de rechtermuisknop op Hallo **Azure AD** Connector en selecteer **Connectorgebied zoeken**.
3. In het pop-upmenu Hallo Connectorgebied zoeken:
    1. Bereik te instellen**in behandeling exporteren**.
    2. Controleer alle 3 selectievakjes, met inbegrip van **toevoegen**, **wijzigen** en **verwijderen**.
    3. Klik op **Search** knop tooreturn alle objecten met wijzigingen die nog toobe geëxporteerd tooAzure AD.
    4. Controleer of dat er zijn geen onverwachte wijzigingen. tooexamine hello wijzigingen voor een bepaald object, dubbelklik op Hallo-object.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>Stap 7. Hallo wijzigingen tooAzure AD exporteren
tooexport hello wijzigingen tooAzure AD:
1. Ga toohello **Connectors** tabblad in Hallo Synchronization Service Manager.
2. Met de rechtermuisknop op Hallo **Azure AD** Connector en selecteer **uitvoeren...**
4. Selecteer in het pop-upmenu Hallo Connector uitvoeren, **exporteren** stap en klik op **OK**.
5. Wacht tot Export tooAzure AD toocomplete en er zijn geen fouten meer LargeObject zijn bevestigen.

### <a name="step-8-re-enable-sync-scheduler"></a>Stap 8. Sync scheduler opnieuw inschakelen
Nu dat Hallo probleem is opgelost, schakelt u Hallo ingebouwde sync scheduler:
1. Start PowerShell-sessie.
2. Geplande synchronisatie opnieuw inschakelen door de cmdlet uit te voeren:`Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Hallo zijn voorgaande stappen alleen van toepassing toonewer versies (1.1.xxx.x) van Azure AD Connect met ingebouwde scheduler Hallo. Als u gebruikmaakt van oudere versies (1.0.xxx.x) van Azure AD Connect die gebruikmaakt van Windows Taakplanner of u uw eigen aangepaste scheduler (niet-algemene) tootrigger periodieke synchronisatie gebruikt, moet u toodisable ze dienovereenkomstig.

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).

