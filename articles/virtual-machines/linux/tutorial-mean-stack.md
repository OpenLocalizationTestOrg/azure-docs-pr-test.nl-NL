---
title: Maken van een gemiddelde stack op een Linux VM in Azure | Microsoft Docs
description: Informatie over het maken van een stack MongoDB, snelle AngularJS en Node.js (gemiddelde) op een Linux VM in Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 892d3481b4ec70fb8434cb25013c5cfd8ab85051
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="92334-103">Maak een stack MongoDB, snelle AngularJS en Node.js (gemiddelde) op een Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="92334-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="92334-104">Deze zelfstudie laat zien hoe u een stack MongoDB, snelle AngularJS en Node.js (gemiddelde) implementeren op een Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="92334-104">This tutorial shows you how to implement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="92334-105">De gemiddelde stack die u maakt kan toevoegen, verwijderen en het weergeven van rapporten in een database.</span><span class="sxs-lookup"><span data-stu-id="92334-105">The MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="92334-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="92334-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="92334-107">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="92334-107">Create a Linux VM</span></span>
> * <span data-ttu-id="92334-108">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="92334-108">Install Node.js</span></span>
> * <span data-ttu-id="92334-109">MongoDB installeren en instellen van de server</span><span class="sxs-lookup"><span data-stu-id="92334-109">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="92334-110">Express installeren en instellen van de routes naar de server</span><span class="sxs-lookup"><span data-stu-id="92334-110">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="92334-111">Toegang tot de routes met AngularJS</span><span class="sxs-lookup"><span data-stu-id="92334-111">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="92334-112">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="92334-112">Run the application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="92334-113">Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="92334-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="92334-114">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="92334-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="92334-115">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="92334-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="92334-116">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="92334-116">Create a Linux VM</span></span>

<span data-ttu-id="92334-117">Maak een resourcegroep met de [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht en maak een Linux-VM met de [az vm maken](https://docs.microsoft.com/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="92334-117">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="92334-118">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="92334-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="92334-119">Het volgende voorbeeld wordt de Azure CLI voor het maken van een resourcegroep met de naam *myResourceGroupMEAN* in de *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="92334-119">The following example uses the Azure CLI to create a resource group named *myResourceGroupMEAN* in the *eastus* location.</span></span> <span data-ttu-id="92334-120">Een virtuele machine gemaakt met de naam *myVM* met SSH-sleutels als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="92334-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="92334-121">Als u een specifieke set van sleutels, gebruikt de--ssh-sleutel / waarde-optie.</span><span class="sxs-lookup"><span data-stu-id="92334-121">To use a specific set of keys, use the --ssh-key-value option.</span></span>

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

<span data-ttu-id="92334-122">Wanneer de virtuele machine is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="92334-122">When the VM has been created, the Azure CLI shows information similar to the following example:</span></span> 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
<span data-ttu-id="92334-123">Noteer het `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="92334-123">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="92334-124">Dit adres wordt gebruikt voor toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="92334-124">This address is used to access the VM.</span></span>

<span data-ttu-id="92334-125">Gebruik de volgende opdracht voor het maken van een SSH-sessie met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="92334-125">Use the following command to create an SSH session with the VM.</span></span> <span data-ttu-id="92334-126">Zorg ervoor dat de juiste openbare IP-adres gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92334-126">Make sure to use the correct public IP address.</span></span> <span data-ttu-id="92334-127">In ons voorbeeld boven onze IP is adres 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="92334-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="92334-128">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="92334-128">Install Node.js</span></span>

<span data-ttu-id="92334-129">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime gebouwd op van de Chrome V8 JavaScript-engine.</span><span class="sxs-lookup"><span data-stu-id="92334-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="92334-130">Node.js wordt gebruikt in deze zelfstudie voor het instellen van de Express-routes en de AngularJS-domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="92334-130">Node.js is used in this tutorial to set up the Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="92334-131">Installeer op de virtuele machine met behulp van de bash-shell die u hebt geopend met SSH, Node.js.</span><span class="sxs-lookup"><span data-stu-id="92334-131">On the VM, using the bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-the-server"></a><span data-ttu-id="92334-132">MongoDB installeren en instellen van de server</span><span class="sxs-lookup"><span data-stu-id="92334-132">Install MongoDB and set up the server</span></span>
<span data-ttu-id="92334-133">[MongoDB](http://www.mongodb.com) -gegevens opslaat in flexibele, zoals JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="92334-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="92334-134">Velden in een database document naar kunnen variëren en gegevensstructuur na verloop van tijd kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="92334-134">Fields in a database can vary from document to document and data structure can be changed over time.</span></span> <span data-ttu-id="92334-135">Voor onze voorbeeldtoepassing toevoegen we adresboekrecords aan MongoDB die rapportnaam, isbn nummer, auteur en het aantal pagina's bevatten.</span><span class="sxs-lookup"><span data-stu-id="92334-135">For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="92334-136">Stel op de virtuele machine met behulp van de bash-shell die u hebt geopend met SSH, de MongoDB-sleutel.</span><span class="sxs-lookup"><span data-stu-id="92334-136">On the VM, using the bash shell that you opened with SSH, set the MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="92334-137">De package manager bijwerken met de sleutel.</span><span class="sxs-lookup"><span data-stu-id="92334-137">Update the package manager with the key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="92334-138">MongoDB installeren.</span><span class="sxs-lookup"><span data-stu-id="92334-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="92334-139">Start de server.</span><span class="sxs-lookup"><span data-stu-id="92334-139">Start the server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="92334-140">Er moet ook installeren de [hoofdtekst parser](https://www.npmjs.com/package/body-parser-json) pakket om ons verwerken van de JSON aanvragen doorgegeven aan de server te helpen.</span><span class="sxs-lookup"><span data-stu-id="92334-140">We also need to install the [body-parser](https://www.npmjs.com/package/body-parser-json) package to help us process the JSON passed in requests to the server.</span></span>

    <span data-ttu-id="92334-141">Installeer de npm package manager.</span><span class="sxs-lookup"><span data-stu-id="92334-141">Install the npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="92334-142">Installeer het pakket van de parser hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="92334-142">Install the body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="92334-143">Maak een map met de naam *Books* en voeg een bestand toe met de naam *server.js* die de configuratie voor de webserver bevat.</span><span class="sxs-lookup"><span data-stu-id="92334-143">Create a folder named *Books* and add a file to it named *server.js* that contains the configuration for the web server.</span></span>

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-to-the-server"></a><span data-ttu-id="92334-144">Express installeren en instellen van de routes naar de server</span><span class="sxs-lookup"><span data-stu-id="92334-144">Install Express and set up routes to the server</span></span>

<span data-ttu-id="92334-145">[Express](https://expressjs.com) is een minimaal en flexibel Node.js web application framework met functies voor webtoepassingen en mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="92334-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="92334-146">Snelle in deze zelfstudie wordt gebruikt om door te geven voor het adresboek van gegevens van en naar onze MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="92334-146">Express is used in this tutorial to pass book information to and from our MongoDB database.</span></span> <span data-ttu-id="92334-147">[Mongoose](http://mongoosejs.com) biedt een ongecompliceerde, schema's gebaseerde oplossing om te modelleren uw toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="92334-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution to model your application data.</span></span> <span data-ttu-id="92334-148">Mongoose wordt gebruikt in deze zelfstudie voor het bieden van een boek-schema voor de database.</span><span class="sxs-lookup"><span data-stu-id="92334-148">Mongoose is used in this tutorial to provide a book schema for the database.</span></span>

1. <span data-ttu-id="92334-149">Snelle en Mongoose installeren.</span><span class="sxs-lookup"><span data-stu-id="92334-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="92334-150">In de *Books* map, maak een map met de naam *apps* en toevoegen van een bestand met de naam *routes.js* van de expliciete routes gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="92334-150">In the *Books* folder, create a folder named *apps* and add a file named *routes.js* with the express routes defined.</span></span>

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted the book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. <span data-ttu-id="92334-151">In de *apps* map, maak een map met de naam *modellen* en toevoegen van een bestand met de naam *book.js* met de adresboek Modelconfiguratie gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="92334-151">In the *apps* folder, create a folder named *models* and add a file named *book.js* with the book model configuration defined.</span></span>  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-the-routes-with-angularjs"></a><span data-ttu-id="92334-152">Toegang tot de routes met AngularJS</span><span class="sxs-lookup"><span data-stu-id="92334-152">Access the routes with AngularJS</span></span>

<span data-ttu-id="92334-153">[AngularJS](https://angularjs.org) biedt een webframework voor het maken van weergaven in uw webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="92334-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="92334-154">In deze zelfstudie gebruiken we AngularJS om verbinding te onze webpagina snelle en acties uitvoeren op onze adresboek-database.</span><span class="sxs-lookup"><span data-stu-id="92334-154">In this tutorial, we use AngularJS to connect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="92334-155">Wijzig de map back-up naar *Books* (`cd ../..`), en maak vervolgens een map met de naam *openbare* en toevoegen van een bestand met de naam *script.js* met de configuratie van de domeincontroller gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="92334-155">Change the directory back up to *Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with the controller configuration defined.</span></span>

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. <span data-ttu-id="92334-156">In de *openbare* map, maakt u een bestand met de naam *index.html* met de webpagina die is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="92334-156">In the *public* folder, create a file named *index.html* with the web page defined.</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-the-application"></a><span data-ttu-id="92334-157">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="92334-157">Run the application</span></span>

1. <span data-ttu-id="92334-158">Wijzig de map back-up naar *Books* (`cd ..`) en start de server door het uitvoeren van deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="92334-158">Change the directory back up to *Books* (`cd ..`) and start the server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="92334-159">Open een webbrowser naar het adres dat u hebt vastgelegd voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="92334-159">Open a web browser to the address that you recorded for the VM.</span></span> <span data-ttu-id="92334-160">Bijvoorbeeld: *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="92334-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="92334-161">U ziet dat lijkt op de volgende pagina:</span><span class="sxs-lookup"><span data-stu-id="92334-161">You should see something like the following page:</span></span>

    ![Book record](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="92334-163">Gegevens invoeren in de tekstvakken en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="92334-163">Enter data into the textboxes and click **Add**.</span></span> <span data-ttu-id="92334-164">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="92334-164">For example:</span></span>

    ![Book record toevoegen](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="92334-166">Na de pagina te vernieuwen, ziet u dat lijkt op deze pagina:</span><span class="sxs-lookup"><span data-stu-id="92334-166">After refreshing the page, you should see something like this page:</span></span>

    ![Lijst adresboekrecords](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="92334-168">U kunt klikken **verwijderen** en de book record verwijderen uit de database.</span><span class="sxs-lookup"><span data-stu-id="92334-168">You could click **Delete** and remove the book record from the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92334-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92334-169">Next steps</span></span>

<span data-ttu-id="92334-170">In deze zelfstudie maakt u een webtoepassing waarin wordt bijgehouden adresboek registreert met behulp van een gemiddelde gemaakt stack op een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="92334-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="92334-171">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="92334-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="92334-172">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="92334-172">Create a Linux VM</span></span>
> * <span data-ttu-id="92334-173">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="92334-173">Install Node.js</span></span>
> * <span data-ttu-id="92334-174">MongoDB installeren en instellen van de server</span><span class="sxs-lookup"><span data-stu-id="92334-174">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="92334-175">Express installeren en instellen van de routes naar de server</span><span class="sxs-lookup"><span data-stu-id="92334-175">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="92334-176">Toegang tot de routes met AngularJS</span><span class="sxs-lookup"><span data-stu-id="92334-176">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="92334-177">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="92334-177">Run the application</span></span>

<span data-ttu-id="92334-178">Ga naar de volgende zelfstudie voor meer informatie over het beveiligen van webservers met SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="92334-178">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92334-179">Webserver met SSL beveiligde</span><span class="sxs-lookup"><span data-stu-id="92334-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
