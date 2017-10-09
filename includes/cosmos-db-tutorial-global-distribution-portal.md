
U kunt meer informatie over Azure Cosmos DB globale distributiepunten in deze Azure vrijdag video met Scott Hanselman en Principal Engineering Manager Karthik Raman.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Zie voor meer informatie over hoe globale databasereplicatie in Cosmos DB werkt, [Distribueer gegevens globaal met Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Globale database gebieden met hello Azure-Portal toevoegen
Azure Cosmos DB is beschikbaar in alle [Azure-regio's] [ azureregions] wereldwijd. Na het selecteren van Hallo standaardniveau consistentie voor het account van uw database, koppelt u een of meer regio's (afhankelijk van uw keuze standaard consistentie niveau en globale distributie moet).

1. In Hallo [Azure-portal](https://portal.azure.com/), Hallo linkerbalk in, klik op **Azure Cosmos DB**.
2. In Hallo **Azure Cosmos DB** blade, selecteer Hallo database account toomodify.
3. Klik in de blade Hallo-account op **globaal gegevens repliceren** in Hallo-menu.
4. In Hallo **globaal gegevens repliceren** blade Hallo regio's tooadd selecteren of door te klikken op gebieden in kaart Hallo verwijderen en klik vervolgens op **opslaan**. Er is een kosten tooadding regio's, raadpleegt u Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/documentdb/) of Hallo [Distribueer gegevens globaal met DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) artikel voor meer informatie.
   
    ![Hallo gebieden in Hallo kaart tooadd klikt u op of verwijder ze][1]
    
Als u een tweede regio toevoegt, Hallo **handmatige Failover** optie is ingeschakeld op Hallo **globaal gegevens repliceren** blade in Hallo-portal. U kunt dit proces optie tootest Hallo failover gebruiken of Hallo primaire schrijven regio wijzigen. Als u een derde regio toevoegt, Hallo **Failover prioriteiten** optie is ingeschakeld op dezelfde blade Hallo zodat u kunt Hallo failover-volgorde voor leesbewerkingen wijzigen.  

### <a name="selecting-global-database-regions"></a>Globale database regio's selecteren
Er zijn twee algemene scenario's voor het configureren van twee of meer gebieden:

1. Lage latentie toegang leveren toodata tooend gebruikers ongeacht waar ze zich hele Hallo wereld bevinden
2. Toevoegen van regionale tolerantie voor bedrijfscontinuïteit en herstel na noodgevallen (BCDR)

Voor gebruikers-leveren lage latentie tooend, wordt aangeraden toodeploy beide toepassing hello en toe te voegen Azure Cosmos DB in regio's Hallo behorend toowhere Hallo toepassing gebruikers zich bevinden.

BCDR, wordt aangeraden tooadd regio's op basis van Hallo regio paren beschreven in Hallo [zakelijke continuïteit en herstel na noodgevallen (BCDR): Azure-gebieden gekoppeld] [ bcdr] artikel.

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
