---
title: aaaConfiguring uw Azure-project met behulp van serviceconfiguraties met meerdere | Microsoft Docs
description: Meer informatie over hoe tooconfigure een Azure-serviceproject cloud door Hallo ServiceDefinition.csdef en ServiceConfiguration.cscfg bestanden wijzigen.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Uw Azure-Project met behulp van serviceconfiguraties met meerdere configureren
Een Azure-cloud service-project bevat twee configuratiebestanden: ServiceDefinition.csdef en ServiceConfiguration.cscfg. Deze bestanden zijn verpakt met uw Azure-cloud service-toepassing en tooAzure geïmplementeerd.

* Hallo **ServiceDefinition.csdef** bestand Hallo metagegevens bevat die is vereist voor hello Azure-omgeving voor Hallo vereisten van uw servicetoepassing cloud, met inbegrip van welke rollen deze bevat. Dit bestand bevat ook configuratie-instellingen die van toepassing zijn tooall exemplaren. Deze configuratie-instellingen kunnen worden gelezen tijdens runtime hello Azure Service Hosting-Runtime-API gebruiken. Dit bestand kan niet worden bijgewerkt terwijl uw service wordt uitgevoerd in Azure.
* Hallo **ServiceConfiguration.cscfg** bestand waarden voor het Hallo configuratie-instellingen is gedefinieerd in het servicedefinitiebestand hello en geeft het aantal exemplaren toorun voor elke rol Hallo. Dit bestand kan worden bijgewerkt terwijl uw cloudservice wordt uitgevoerd in Azure.

Hello Azure's voor Microsoft Visual Studio bieden eigenschappenpagina's die u kunt tooset configuratie-instellingen opgeslagen in deze bestanden gebruiken. tooaccess Hallo eigenschappenvensters, dubbelklik op Hallo rol verwijzing onder hello Azure cloud service-project in Solution Explorer of met de rechtermuisknop op Hallo rol verwijzing en kiest u **eigenschappen**, zoals weergegeven in de volgende afbeelding Hallo.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Zie voor informatie over Hallo schema's voor de servicedefinitie Hallo en configuratiebestanden van de service onderliggende hello [schemaverwijzing](https://msdn.microsoft.com/library/azure/dd179398.aspx). Zie voor meer informatie over de serviceconfiguratie van de [hoe tooConfigure Cloud Services](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Eigenschappen van de rol configureren
Hallo eigenschappenpagina's voor een Webrol en een werkrol zijn vergelijkbaar, maar er een paar verschillen zijn, uiteengezet in Hallo uit te voeren.

Van Hallo **opslaan in cache** pagina die u kunt configureren hello Azure caching-services.

### <a name="configuration-page"></a>Configuratiepagina
Op Hallo **configuratie** pagina kunt u deze eigenschappen instellen:

**Exemplaren**

Set Hallo **exemplaar** eigenschap toohello aantal exemplaren Hallo-service moet worden uitgevoerd voor deze rol.

Set Hallo **VM-grootte** eigenschap te**Extra klein**, **kleine**, **gemiddeld**, **grote**, of **Extra groot**.  Zie voor meer informatie [grootten voor Cloudservices](cloud-services/cloud-services-sizes-specs.md).

**Opstartactie** (rol alleen Web)

Stel deze eigenschap toospecify die Visual Studio een webbrowser voor eindpunten Hallo HTTP of HTTPS-eindpunten Hallo of beide moet worden gestart als u foutopsporing start.

Hallo HTTPS-eindpunt-optie is alleen beschikbaar als u al een HTTPS-eindpunt voor de rol hebt gedefinieerd. U kunt een HTTPS-eindpunt op Hallo definiëren **eindpunten** eigenschappenpagina.

Als u al een HTTPS-eindpunt hebt toegevoegd, Hallo HTTPS-eindpunt-optie is standaard ingeschakeld en Visual Studio een browser voor dit eindpunt wordt gestart bij het starten van foutopsporing bovendien tooa browser voor uw HTTP-eindpunt. Hierbij wordt ervan uitgegaan dat beide opstartopties zijn ingeschakeld.

**Diagnostics**

Diagnostische gegevens is standaard ingeschakeld voor de Webrol Hallo. Hello Azure cloud service-project en storage-account zijn ingesteld toouse Hallo lokale opslagemulator. Wanneer u klaar toodeploy tooAzure bent, kunt u Hallo builder knop (**...** ) tooupdate Hallo storage account toouse Azure Hallo cloud-opslag. Hallo diagnostische gegevens toohello storage-account kunnen worden overgedragen op aanvraag of automatisch geplande intervallen. Zie voor meer informatie over Azure diagnostics [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Pagina met instellingen
Op Hallo **instellingen** pagina kunt u de configuratie-instellingen voor uw service toevoegen. Configuratie-instellingen zijn naam / waarde-paren. Code die wordt uitgevoerd in de rol Hallo Hallo waarden van uw configuratie-instellingen bij uitvoering met klassen die worden geleverd door Hallo kan lezen [Azure beheerde bibliotheek](http://go.microsoft.com/fwlink?LinkID=171026). In het bijzonder Hallo [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) methode retourneert Hallo-waarde van een benoemde configuratie-instelling tijdens runtime.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Een verbinding tekenreeks tooa storage-account configureren
Een verbindingsreeks is een configuratie-instelling waarmee verbinding en verificatiegegevens voor de opslagemulator Hallo of voor een Azure storage-account. Wanneer uw code toegang moet hebben tot Azure storage services gegevens – dat wil zeggen, blob, wachtrij of tabelgegevens van de code die wordt uitgevoerd in een rol, hebt u toodefine een verbindingsreeks voor dat opslagaccount.

Een verbindingsreeks die tooan Azure storage-account wijst moet een gedefinieerde indeling gebruiken. Voor informatie over het toocreate verbindingsreeksen, Zie [Azure Storage-verbindingsreeksen configureren](storage/common/storage-configure-connection-string.md).

Wanneer u klaar tootest uw service tegen hello Azure storage-services, of wanneer u bent klaar toodeploy uw cloud service tooAzure, kunt u Hallo-waarde van een verbinding tekenreeksen toopoint tooyour Azure storage-account wijzigen. Selecteer (**...** ), selecteer **opslagaccountreferenties Voer**. Voer uw accountgegevens die uw accountnaam en accountsleutel bevat. In Hallo **Storage Account Connection String** in het dialoogvenster kunt u ook aangeven of u toouse Hallo standaard HTTPS-eindpunten (standaardoptie Hallo), Hallo standaard HTTP-eindpunten of aangepaste eindpunten wilt. U kunt aangepaste eindpunten toouse besluiten als u een aangepaste domeinnaam voor uw service geregistreerd zoals beschreven in [een aangepaste domeinnaam configureren voor blob-gegevens in Azure storage-account](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Voordat u uw service implementeert, moet u uw verbinding tekenreeksen toopoint tooan Azure storage-account wijzigen. Mislukt toodo dit kan ertoe leiden dat uw rol niet toostart of toocycle via Hallo statussen initialiseren bezet en stoppen.
> 
> 

## <a name="endpoints-page"></a>Pagina eindpunten
Een werkrol kan een onbeperkt aantal HTTP-, HTTPS- of TCP-eindpunten hebben. Eindpunten kunnen invoereindpunten beschikbaar tooexternal clients zijn, of interne eindpunten die beschikbaar tooother-functies die worden uitgevoerd in Hallo-service zijn.

* toomake een HTTP-eindpunt beschikbaar tooexternal clients webbrowsers Hallo eindpunt type tooinput wijzigen en geef een naam en een openbare-poortnummer.
* een HTTPS-toomake endpoint beschikbaar tooexternal-clients en webbrowsers, Hallo eindpunttype ook wijzigen**invoer**, en geef een naam, een openbare-poortnummer en de naam van een management-certificaat.
  
    Opmerking voordat u een beheercertificaat opgeven kunt, u Hallo certificaat op Hallo definiëren moet **certificaten** eigenschappenpagina.
* toomake een eindpunt beschikbaar voor interne toegang door andere functies in Hallo-cloudservice, Hallo eindpunt type toointernal wijzigen en geef een naam en mogelijke particuliere poorten voor dit eindpunt.

## <a name="local-storage-page"></a>Lokale opslag-pagina
U kunt Hallo **lokale opslag** eigenschap pagina tooreserve een of meer resources voor lokale opslag voor een rol. Een resource lokale opslag is een gereserveerde map in het bestandssysteem Hallo Hallo Azure virtuele machine in een exemplaar van een rol wordt uitgevoerd.

## <a name="certificates-page"></a>De pagina Certificaten
Op Hallo **certificaten** pagina u certificaten kunt koppelen aan uw rol. Hallo-certificaten die u toevoegt, mag gebruikte tooconfigure uw HTTPS-eindpunten op Hallo **eindpunten** eigenschappenpagina.

Hallo **certificaten** eigenschappenpagina wordt informatie over de configuratie van uw certificaten tooyour service toegevoegd. Houd er rekening mee dat uw certificaten niet zijn verpakt met uw service; u moet uw certificaten afzonderlijk uploaden tooAzure via Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate een certificaat met de rol, Geef een naam voor Hallo certificaat. U gebruikt dit certificaat naam toorefer toohello wanneer u een HTTPS-eindpunt op Hallo configureert **eindpunten** eigenschappenpagina. Vervolgens opgeven of het certificaatarchief Hallo **lokale Machine** of **huidige gebruiker** en Hallo-naam van Hallo store. Voer ten slotte Hallo certificaatvingerafdruk. Als Hallo certificaat in de huidige User\Personal hello () winkel, kunt u Hallo certificaatvingerafdruk door het Hallo-certificaat van een ingevulde lijst te selecteren. Als deze zich op een andere locatie, voert u Hallo vingerafdrukwaarde handmatig in.

Wanneer u een certificaat uit het certificaatarchief Hallo toevoegt, worden alle tussenliggende certificaten toohello configuratie-instellingen voor u automatisch toegevoegd. Deze tussenliggende certificaten moeten ook worden geüpload tooAzure in volgorde toocorrectly uw service voor SSL configureren.

Van beheercertificaten die u aan uw service koppelen tooyour service alleen toegepast wanneer deze wordt uitgevoerd in de cloud Hallo. Wanneer uw service wordt uitgevoerd in de lokale ontwikkelingsomgeving hello, gebruikt een standaardcertificaat dat wordt beheerd door Hallo rekenemulator.

## <a name="configuring-hello-azure-cloud-service-project"></a>Hello Azure cloud service-project configureren
tooconfigure-instellingen die van toepassing tooan volledige Azure-cloud service-project, u het snelmenu Hallo voor dat projectknooppunt eerst opent en vervolgens kiest u eigenschappen tooopen de eigenschappenvensters. Hallo volgende tabel ziet u de eigenschappenpagina's.

| Eigenschappenpagina | Beschrijving |
| --- | --- |
| Toepassing |Op deze pagina kunt u informatie over het Hallo-versie van Azure-hulpprogramma's die gebruikmaakt van deze cloudserviceproject weergeven en u de huidige versie toohello Hallo-hulpprogramma's kunt upgraden. |
| Gebeurtenissen maken |Op deze pagina kunt u gebeurtenissen vóór het samenstellen en na het samenstellen instellen. |
| Ontwikkeling |Op deze pagina kunt u configuratie-instructies build en Hallo voorwaarden waaronder alle gebeurtenissen na build worden uitgevoerd. |
| Web |Op deze pagina kunt u de instellingen die betrekking toohello webserver hebben configureren. |

