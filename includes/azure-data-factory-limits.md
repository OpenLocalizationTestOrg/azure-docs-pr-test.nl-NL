Gegevensfactory is een multitenant-service die beschikt over de volgende standaardlimiet om ervoor te zorgen klantabonnementen zijn beveiligd tegen elkaars werkbelastingen. Veel van de limieten kunnen eenvoudig gegeven voor uw abonnement tot het maximum aantal contact opnemen met de ondersteuning.

| **Resource** | **Standaardlimiet** | **Maximumaantal** |
| --- | --- | --- |
| Data Factory's in een Azure-abonnement |50 |[Contact opnemen met ondersteuning](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| pijplijnen binnen een gegevensfactory |2500 |[Contact opnemen met ondersteuning](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| gegevenssets binnen een gegevensfactory |5000 |[Contact opnemen met ondersteuning](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| gelijktijdige segmenten per gegevensset |10 |10 |
| aantal bytes per object voor pipeline-objecten <sup>1</sup> |200 KB |200 KB |
| aantal bytes per object voor de gegevensset en objecten van de gekoppelde service <sup>1</sup> |100 KB |2000 KB |
| HDInsight-cluster op aanvraag kernen binnen een abonnement <sup>2</sup> |60 |[Contact opnemen met ondersteuning](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| De verplaatsing gegevenseenheid cloud <sup>3</sup> |32 |[Contact opnemen met ondersteuning](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Aantal voor pijplijn activiteiten bij uitvoering nieuwe pogingen |1000 |MaxInt (32 bits) |

<sup>1</sup> pipeline, gegevensset en objecten van de gekoppelde service vertegenwoordigen een logische groepering van uw workload. Limieten voor deze objecten geen betrekking hebben op de hoeveelheid gegevens die u kunt verplaatsen en met de Azure Data Factory-service verwerken. Gegevensfactory is ontworpen om te schalen voor petabytes aan gegevens.

<sup>2</sup> on-demand HDInsight-kernen worden toegewezen uit het abonnement dat u de gegevensfactory bevat. Als gevolg hiervan is de bovenstaande limiet voor de Data Factory afgedwongen limiet kernen voor bellen op HDInsight kernen en verschilt van de core limiet die is gekoppeld aan uw Azure-abonnement.

<sup>3</sup> cloud gegevensverplaatsing gegevenseenheid (DMU) wordt gebruikt in een cloud-naar-cloud kopieerbewerking. Is een meting met de kracht (een combinatie van CPU, geheugen en netwerkresourcetoewijzing) van één eenheid in de Data Factory. Dankzij het gebruik van meer DMUs voor sommige scenario's kunt u hogere kopie doorvoer behalen. Raadpleeg [Cloud data movement eenheden](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) sectie voor meer informatie.

| **Resource** | **De ondergrens standaard** | **Minimale limiet** |
| --- | --- | --- |
| Plannen van interval |15 minuten |15 minuten |
| Interval tussen nieuwe pogingen |1 seconde |1 seconde |
| Probeer de time-outwaarde |1 seconde |1 seconde |

### <a name="web-service-call-limits"></a>Limieten voor aanroep van Web service
Azure Resource Manager heeft limieten voor API-aanroepen. U kunt de API-aanroepen maken met een frequentie binnen de [Azure Resource Manager-API beperkt](../articles/azure-subscription-service-limits.md#resource-group-limits).
