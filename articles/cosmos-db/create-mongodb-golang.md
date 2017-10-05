---
title: 'Azure Cosmos DB: een MongoDB-API-console-app ontwikkelen met Golang en Azure Portal | Microsoft Docs'
description: Is een Golang-codevoorbeeld dat u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit Azure Cosmos DB
services: cosmos-db
author: Durgaprasad-Budhwani
manager: jhubbard
editor: mimig1
ms.service: cosmos-db
ms.topic: hero-article
ms.date: 07/21/2017
ms.author: mimig
ms.openlocfilehash: 9461a5d86b321fd02167379ba8751d44a861ebc2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-the-azure-portal"></a><span data-ttu-id="1759e-103">Azure Cosmos DB: een MongoDB-API-console-app ontwikkelen met Golang en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1759e-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal</span></span>

<span data-ttu-id="1759e-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1759e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1759e-105">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafieken en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de globale distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1759e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="1759e-106">In deze Quick Start ziet u hoe u een bestaande, in [Golang](https://golang.org/) geschreven [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction)-app kunt gebruiken en verbinden met uw Azure Cosmos DB-database, die MongoDB-clientverbindingen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="1759e-106">This quick-start demonstrates how to use an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it to your Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="1759e-107">Met andere woorden, uw Golang-toepassing weet alleen dat deze wordt verbonden met een database met behulp van MongoDB-API's.</span><span class="sxs-lookup"><span data-stu-id="1759e-107">In other words, your Golang application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="1759e-108">Het is duidelijk voor de toepassing dat de gegevens worden opgeslagen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1759e-108">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1759e-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1759e-109">Prerequisites</span></span>

- <span data-ttu-id="1759e-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1759e-110">An Azure subscription.</span></span> <span data-ttu-id="1759e-111">Als u nog geen abonnement op Azure hebt, maakt u een [gratis account](https://azure.microsoft.com/free) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="1759e-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="1759e-112">[Go](https://golang.org/dl/) en basiskennis van de [Go](https://golang.org/)-taal.</span><span class="sxs-lookup"><span data-stu-id="1759e-112">[Go](https://golang.org/dl/) and a basic knowledge of the [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="1759e-113">Een IDE: [Gogland](https://www.jetbrains.com/go/) van Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) van Microsoft of [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="1759e-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="1759e-114">In deze zelfstudie wordt Goglang gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1759e-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="1759e-115">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="1759e-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="1759e-116">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="1759e-116">Clone the sample application</span></span>

<span data-ttu-id="1759e-117">Kloon de voorbeeldtoepassing en installeer de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="1759e-117">Clone the sample application and install the required packages.</span></span>

1. <span data-ttu-id="1759e-118">Maak een map met de naam CosmosDBSample in de map GOROOT\src. Standaard heet de map C:\Go\.</span><span class="sxs-lookup"><span data-stu-id="1759e-118">Create a folder named CosmosDBSample inside the GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="1759e-119">Voer de volgende opdracht uit met een Git-terminalvenster zoals Git-bash om de voorbeeldopslagplaats te klonen in de map CosmosDBSample.</span><span class="sxs-lookup"><span data-stu-id="1759e-119">Run the following command using a git terminal window such as git bash to clone the sample repository into the CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="1759e-120">Voer de volgende opdracht uit om het mgo-pakket op te halen.</span><span class="sxs-lookup"><span data-stu-id="1759e-120">Run the following command to get the mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="1759e-121">Het [mgo](http://labix.org/mgo)-stuurprogramma (uitgesproken als *mango*) is een [MongoDB](http://www.mongodb.org/)-stuurprogramma voor de [Go-taal](http://golang.org/). Hiermee wordt een uitgebreide en goed geteste reeks functies geïmplementeerd op basis van een heel eenvoudige API die is voorzien van standaard-Go-terminologie.</span><span class="sxs-lookup"><span data-stu-id="1759e-121">The [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for the [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="1759e-122">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="1759e-122">Update your connection string</span></span>

<span data-ttu-id="1759e-123">Ga nu terug naar Azure Portal om de verbindingsreeksinformatie op te halen en kopieer deze in de app.</span><span class="sxs-lookup"><span data-stu-id="1759e-123">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="1759e-124">Klik op **Snel starten** in het navigatiemenu links en klik op **Overige** om de verbindingstekenreeksinformatie te bekijken die is vereist voor de Go-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1759e-124">Click **Quick start** in the left navigation menu, and then click **Other** to view the connection string information required by the Go application.</span></span>

2. <span data-ttu-id="1759e-125">In Goglang opent u het bestand main.go in de map GOROOT\CosmosDBSample. Werk de volgende regels code bij met de verbindingstekenreeksinformatie uit Azure Portal, zoals in de volgende schermafbeelding te zien is.</span><span class="sxs-lookup"><span data-stu-id="1759e-125">In Goglang, open the main.go file in the GOROOT\CosmosDBSample directory and update the following lines of code using the connection string information from the Azure portal as shown in the following screenshot.</span></span> 

    <span data-ttu-id="1759e-126">De naam van de database is het voorvoegsel van de waarde **Host** in het deelvenster met de verbindingstekenreeks in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1759e-126">The Database name is the prefix of the **Host** value in the Azure portal connection string pane.</span></span> <span data-ttu-id="1759e-127">Voor het account dat in de onderstaande afbeelding wordt weergegeven, is de databasenaam golang-coach.</span><span class="sxs-lookup"><span data-stu-id="1759e-127">For the account shown in the image below, the Database name is golang-coach.</span></span>

    ```go
    Database: "The prefix of the Host value in the Azure portal",
    Username: "The Username in the Azure portal",
    Password: "The Password in the Azure portal",
    ```

    ![Deelvenster Snel starten, tabblad Overige in Azure Portal met daarin de verbindingstekenreeksinformatie](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="1759e-129">Sla het bestand main.go op.</span><span class="sxs-lookup"><span data-stu-id="1759e-129">Save the main.go file.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="1759e-130">De code bekijken</span><span class="sxs-lookup"><span data-stu-id="1759e-130">Review the code</span></span>

<span data-ttu-id="1759e-131">Laten we eens kijken wat er precies gebeurt in het bestand main.go.</span><span class="sxs-lookup"><span data-stu-id="1759e-131">Let's make a quick review of what's happening in the main.go file.</span></span> 

### <a name="connecting-the-go-app-to-azure-cosmos-db"></a><span data-ttu-id="1759e-132">De Go-app verbinden met Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1759e-132">Connecting the Go app to Azure Cosmos DB</span></span>

<span data-ttu-id="1759e-133">Azure Cosmos DB biedt ondersteuning voor MongoDB met SSL ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1759e-133">Azure Cosmos DB supports the SSL-enabled MongoDB.</span></span> <span data-ttu-id="1759e-134">Als u verbinding wilt maken met een MongoDB met SSL, moet u de functie **DialServer** definiëren in [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo) en gebruikmaken van de functie [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) om de verbinding tot stand te laten komen.</span><span class="sxs-lookup"><span data-stu-id="1759e-134">To connect to an SSL-enabled MongoDB, you need to define the **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of the [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function to perform the connection.</span></span>

<span data-ttu-id="1759e-135">Met het volgende Golang-codefragment verbindt u de Go-app met de Azure Cosmos DB MongoDB-API.</span><span class="sxs-lookup"><span data-stu-id="1759e-135">The following Golang code snippet connects the Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="1759e-136">De klasse *DialInfo* bevat opties voor het starten van een sessie met een MongoDB-cluster.</span><span class="sxs-lookup"><span data-stu-id="1759e-136">The *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// to our Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect to mongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes the session safety mode.
// If the safe parameter is nil, the session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. The unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="1759e-137">De methode **mgo.Dial()** wordt gebruikt als er geen SSL-verbinding is.</span><span class="sxs-lookup"><span data-stu-id="1759e-137">The **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="1759e-138">Voor een SSL-verbinding is de methode **mgo.DialWithInfo()** vereist.</span><span class="sxs-lookup"><span data-stu-id="1759e-138">For an SSL connection, the **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="1759e-139">Er wordt een exemplaar van het object **DialWIthInfo {}** gebruikt om het sessieobject te maken.</span><span class="sxs-lookup"><span data-stu-id="1759e-139">An instance of the **DialWIthInfo{}** object is used to create the session object.</span></span> <span data-ttu-id="1759e-140">Zodra de sessie is gestart, kunt u de verzameling openen met het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="1759e-140">Once the session is established, you can access the collection by using the following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="1759e-141">Een document maken</span><span class="sxs-lookup"><span data-stu-id="1759e-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="1759e-142">Query's uitvoeren voor een document of een document lezen</span><span class="sxs-lookup"><span data-stu-id="1759e-142">Query or read a document</span></span>

<span data-ttu-id="1759e-143">Azure Cosmos DB biedt ondersteuning voor uitgebreide query's voor de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="1759e-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="1759e-144">In de volgende voorbeeldcode ziet u een query die u kunt uitvoeren op de documenten in uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="1759e-144">The following sample code shows a query that you can run against the documents in your collection.</span></span>

```go
// Get a Document from the collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="1759e-145">Een document bijwerken</span><span class="sxs-lookup"><span data-stu-id="1759e-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="1759e-146">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="1759e-146">Delete a document</span></span>

<span data-ttu-id="1759e-147">Azure Cosmos DB biedt ondersteuning voor het verwijderen van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="1759e-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-the-app"></a><span data-ttu-id="1759e-148">De app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1759e-148">Run the app</span></span>

1. <span data-ttu-id="1759e-149">In Golang controleert u of uw GOPATH (beschikbaar via **Bestand**, **Instellingen**, **Go**, **GOPATH**) de locatie bevat waarin de gopkg is geïnstalleerd. Standaard is dit USERPROFILE\go.</span><span class="sxs-lookup"><span data-stu-id="1759e-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include the location in which the gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="1759e-150">Markeer de regels waarmee het document wordt verwijderd (regel 91-96) als commentaar, zodat u het document na het uitvoeren van de app kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="1759e-150">Comment out the lines that delete the document, lines 91-96, so that you can see the document after running the app.</span></span>
3. <span data-ttu-id="1759e-151">In Goglang klikt u op **Uitvoeren** en daarna op **'Build main.go and run' uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="1759e-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="1759e-152">De app wordt voltooid en de beschrijving wordt weergegeven van het document dat u hebt gemaakt in [Een document maken](#create-document).</span><span class="sxs-lookup"><span data-stu-id="1759e-152">The app finishes and displays the description of the document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Golang, waarin de uitvoer van de app wordt weergegeven](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="1759e-154">Uw document bekijken in Data Explorer</span><span class="sxs-lookup"><span data-stu-id="1759e-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="1759e-155">Ga terug naar Azure Portal om uw document te bekijken in Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="1759e-155">Go back to the Azure portal to see your document in Data Explorer.</span></span>

1. <span data-ttu-id="1759e-156">Klik op **Data Explorer (Preview)** in het navigatiemenu links, vouw **golang-coach**, **package** uit en klik vervolgens op **Documenten**.</span><span class="sxs-lookup"><span data-stu-id="1759e-156">Click **Data Explorer (Preview)** in the left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="1759e-157">Op het tabblad **Documenten** klikt u op de \_-id om het document in het rechterdeelvenster weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1759e-157">In the **Documents** tab, click the \_id to display the document in the right pane.</span></span> 

    ![Data Explorer waarin het zojuist gemaakte document wordt weergegeven](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="1759e-159">U kunt vervolgens inline met het document werken. Klik op **Bijwerken** om het op te slaan.</span><span class="sxs-lookup"><span data-stu-id="1759e-159">You can then work with the document inline and click **Update** to save it.</span></span> <span data-ttu-id="1759e-160">U kunt het document ook verwijderen of nieuwe documenten of query's aanmaken.</span><span class="sxs-lookup"><span data-stu-id="1759e-160">You can also delete the document, or create new documents or queries.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="1759e-161">SLA’s bekijken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1759e-161">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1759e-162">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="1759e-162">Clean up resources</span></span>

<span data-ttu-id="1759e-163">Als u deze app niet verder gaat gebruiken, kunt u alle resources verwijderen die door deze Quick Start zijn aangemaakt door onderstaande stappen te volgen in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="1759e-163">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="1759e-164">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1759e-164">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="1759e-165">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1759e-165">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1759e-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1759e-166">Next steps</span></span>

<span data-ttu-id="1759e-167">In deze Quick Start hebt u geleerd hoe een Azure Cosmos DB-account kunt maken en een Golang-app kunt uitvoeren met de API voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1759e-167">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Golang app using the API for MongoDB.</span></span> <span data-ttu-id="1759e-168">Nu kunt u aanvullende gegevens in uw Cosmos DB-account importeren.</span><span class="sxs-lookup"><span data-stu-id="1759e-168">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1759e-169">Gegevens importeren in Azure Cosmos DB voor de MongoDB-API</span><span class="sxs-lookup"><span data-stu-id="1759e-169">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)
