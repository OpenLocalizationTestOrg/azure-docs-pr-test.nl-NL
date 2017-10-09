
## <a name="size-table-definitions"></a>De grootte van tabeldefinities wijzigen

- De opslagcapaciteit wordt weergegeven in GiB-eenheden of 1024^3 bytes. Wanneer het vergelijken van schijven gemeten in GB (1000 ^ 3 bytes) toodisks gemeten in GiB (1024 ^ 3) onthouden capaciteit getallen die zijn opgegeven in GiB lijkt kleiner. 1023 GiB is bijvoorbeeld gelijk aan 1098,4 GB
- De schijfdoorvoer wordt gemeten in I/O-bewerkingen per seconde (IOPS) en MBps, waarbij MBps = 10^6 bytes per seconde.
- Gegevensschijven kunnen in de modus met of zonder caching werken. Voor gegevens in de cache schijfbewerking, Hallo host-cachemodus te ingesteld**ReadOnly** of **ReadWrite**.  Voor schijfbewerking uncached gegevens, Hallo host-cachemodus te ingesteld**geen**.
- **Netwerkprestaties verwacht** Hallo maximale cumulatieve bandbreedte is toegewezen per VM-type op alle NIC's voor alle bestemmingen. Bovengrenzen niet worden gegarandeerd, maar zijn bedoeld tooprovide richtlijnen voor het selecteren van Hallo juiste VM-type voor de toepassing hello bedoeld. De werkelijke netwerkprestaties zijn afhankelijk van verschillende factoren, waaronder netwerkcongestie, toepassingsbelastingen en netwerkinstellingen. Zie [Netwerkdoorvoer optimaliseren voor Windows en Linux](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md) voor meer informatie over het optimaliseren van de netwerkdoorvoer. Hallo tooachieve verwacht netwerkprestaties op Linux- of Windows, mogelijk nodig tooselect een specifieke versie of optimaliseren van uw virtuele machine. Zie voor meer informatie [hoe tooreliably testen voor een virtuele machine doorvoer](../articles/virtual-network/virtual-network-bandwidth-testing.md).

- &#8224; 16 vCPU prestaties wordt consistent Hallo bovengrens in een toekomstige release bereiken.


