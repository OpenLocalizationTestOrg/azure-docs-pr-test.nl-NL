Gegevensfactory is een multitenant-service die is Hallo standaardlimiet in place toomake ervoor klantabonnementen zijn beveiligd tegen elkaars werkbelastingen te volgen. Veel Hallo limieten kunnen worden eenvoudig gegenereerd voor uw abonnement van de maximumlimiet toohello door contact op met ondersteuning.

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

<sup>1</sup> pipeline, gegevensset en objecten van de gekoppelde service vertegenwoordigen een logische groepering van uw workload. Tooamount van gegevens die u kunt verplaatsen en met hello Azure Data Factory-service verwerken geen verband houden met beperkingen voor deze objecten. Gegevensfactory is ontworpen tooscale toohandle petabytes aan gegevens.

<sup>2</sup> on-demand HDInsight-kernen worden toegewezen buiten het Hallo-abonnement dat Hallo gegevensfactory bevat. Hallo boven de limiet is als gevolg hiervan Hallo Data Factory afgedwongen limiet kernen voor bellen op HDInsight kernen en verschilt van Hallo core limiet die is gekoppeld aan uw Azure-abonnement.

<sup>3</sup> cloud gegevensverplaatsing gegevenseenheid (DMU) wordt gebruikt in een cloud-naar-cloud kopieerbewerking. Is een meting met Hallo power (een combinatie van CPU, geheugen en netwerkresourcetoewijzing) van één eenheid in de Data Factory. Dankzij het gebruik van meer DMUs voor sommige scenario's kunt u hogere kopie doorvoer behalen. Raadpleeg te[Cloud data movement eenheden](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) sectie voor meer informatie.

| **Resource** | **De ondergrens standaard** | **Minimale limiet** |
| --- | --- | --- |
| Plannen van interval |15 minuten |15 minuten |
| Interval tussen nieuwe pogingen |1 seconde |1 seconde |
| Probeer de time-outwaarde |1 seconde |1 seconde |

### <a name="web-service-call-limits"></a>Limieten voor aanroep van Web service
Azure Resource Manager heeft limieten voor API-aanroepen. U kunt de API-aanroepen maken met een frequentie binnen Hallo [Azure Resource Manager-API beperkt](../articles/azure-subscription-service-limits.md#resource-group-limits).
