---
title: een gemiddelde aaaCreate stack op een Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een MongoDB, snelle AngularJS en Node.js (gemiddelde) stack is op een Linux VM in Azure.
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
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="9e3a3-103">Maak een stack MongoDB, snelle AngularJS en Node.js (gemiddelde) op een Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="9e3a3-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="9e3a3-104">Deze zelfstudie leert u hoe tooimplement een MongoDB, snelle AngularJS en Node.js (gemiddelde) stack is op een Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="9e3a3-105">GEMIDDELDE Hallo-stack die u maakt kan toevoegen, verwijderen en het weergeven van rapporten in een database.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="9e3a3-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="9e3a3-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e3a3-107">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="9e3a3-107">Create a Linux VM</span></span>
> * <span data-ttu-id="9e3a3-108">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="9e3a3-108">Install Node.js</span></span>
> * <span data-ttu-id="9e3a3-109">MongoDB installeren en het Hallo-server instellen</span><span class="sxs-lookup"><span data-stu-id="9e3a3-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="9e3a3-110">Express installeren en routes toohello server instellen</span><span class="sxs-lookup"><span data-stu-id="9e3a3-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="9e3a3-111">Toegang Hallo routes met AngularJS</span><span class="sxs-lookup"><span data-stu-id="9e3a3-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="9e3a3-112">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9e3a3-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9e3a3-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9e3a3-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9e3a3-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9e3a3-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="9e3a3-116">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="9e3a3-116">Create a Linux VM</span></span>

<span data-ttu-id="9e3a3-117">Een resourcegroep maken met de Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht en maak een Linux-VM met Hallo [az vm maken](https://docs.microsoft.com/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="9e3a3-118">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="9e3a3-119">Hallo volgende voorbeeld wordt een resourcegroep met de naam van hello Azure CLI toocreate *myResourceGroupMEAN* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="9e3a3-120">Een virtuele machine gemaakt met de naam *myVM* met SSH-sleutels als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="9e3a3-121">toouse een specifieke set sleutels, gebruik Hallo--ssh-sleutel / waarde-optie.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

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

<span data-ttu-id="9e3a3-122">Wanneer Hallo VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="9e3a3-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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
<span data-ttu-id="9e3a3-123">Let op Hallo `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="9e3a3-124">Dit adres is gebruikte tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="9e3a3-125">Gebruik Hallo volgende opdracht toocreate een SSH-sessie met de Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="9e3a3-126">Zorg ervoor dat toouse Hallo juiste openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="9e3a3-127">In ons voorbeeld boven onze IP is adres 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="9e3a3-128">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="9e3a3-128">Install Node.js</span></span>

<span data-ttu-id="9e3a3-129">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime gebouwd op van de Chrome V8 JavaScript-engine.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="9e3a3-130">Node.js wordt gebruikt in deze zelfstudie tooset Hallo die Express routes en AngularJS-controllers.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="9e3a3-131">Installeer op Hallo VM, met Hallo bash-shell die u hebt geopend met SSH, Node.js.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="9e3a3-132">MongoDB installeren en het Hallo-server instellen</span><span class="sxs-lookup"><span data-stu-id="9e3a3-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="9e3a3-133">[MongoDB](http://www.mongodb.com) -gegevens opslaat in flexibele, zoals JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="9e3a3-134">Velden in een database kunnen afwijken van het document toodocument en gegevensstructuur na verloop van tijd kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="9e3a3-135">Voor onze voorbeeldtoepassing toevoegen we adresboek records tooMongoDB die rapportnaam, isbn nummer, auteur en het aantal pagina's bevatten.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="9e3a3-136">Virtuele machine, met Hallo bash-shell die u hebt geopend met SSH, ingesteld op Hallo Hallo MongoDB-sleutel.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="9e3a3-137">Hallo Pakketbeheer bijwerken met Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="9e3a3-138">MongoDB installeren.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="9e3a3-139">Hallo-server niet starten.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="9e3a3-140">Ook moet tooinstall Hallo [hoofdtekst parser](https://www.npmjs.com/package/body-parser-json) pakket toohelp ons Hallo JSON toohello-server aanvragen doorgegeven verwerken.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="9e3a3-141">Hallo npm Pakketbeheer installeren.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="9e3a3-142">Hallo hoofdtekst parser pakketten installeren.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="9e3a3-143">Maak een map met de naam *Books* en voeg de tooit van een bestand met de naam *server.js* die Hallo-configuratie voor de webserver Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

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

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="9e3a3-144">Express installeren en routes toohello server instellen</span><span class="sxs-lookup"><span data-stu-id="9e3a3-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="9e3a3-145">[Express](https://expressjs.com) is een minimaal en flexibel Node.js web application framework met functies voor webtoepassingen en mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="9e3a3-146">Express wordt gebruikt in deze zelfstudie toopass adresboek informatie tooand uit onze MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="9e3a3-147">[Mongoose](http://mongoosejs.com) biedt een ongecompliceerde, schema's gebaseerde oplossing toomodel uw toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="9e3a3-148">Mongoose wordt gebruikt in deze zelfstudie tooprovide een boek schema voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="9e3a3-149">Snelle en Mongoose installeren.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="9e3a3-150">In Hallo *Books* map, maak een map met de naam *apps* en toevoegen van een bestand met de naam *routes.js* Hello express routes die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

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
            message: "Successfully deleted hello book",
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

3. <span data-ttu-id="9e3a3-151">In Hallo *apps* map, maak een map met de naam *modellen* en toevoegen van een bestand met de naam *book.js* met Hallo adresboek Modelconfiguratie is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

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

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="9e3a3-152">Toegang Hallo routes met AngularJS</span><span class="sxs-lookup"><span data-stu-id="9e3a3-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="9e3a3-153">[AngularJS](https://angularjs.org) biedt een webframework voor het maken van weergaven in uw webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="9e3a3-154">In deze zelfstudie we het gebruik van de AngularJS tooconnect onze webpagina snelle en acties uitvoeren op onze adresboek-database.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="9e3a3-155">Hallo directory ook een back-up wijzigen*Books* (`cd ../..`), en maak vervolgens een map met de naam *openbare* en toevoegen van een bestand met de naam *script.js* met Hallo-controller de configuratie is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

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
    
2. <span data-ttu-id="9e3a3-156">In Hallo *openbare* map, maakt u een bestand met de naam *index.html* met Hallo webpagina gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

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

##  <a name="run-hello-application"></a><span data-ttu-id="9e3a3-157">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9e3a3-157">Run hello application</span></span>

1. <span data-ttu-id="9e3a3-158">Hallo directory ook een back-up wijzigen*Books* (`cd ..`) en het Hallo-server starten met deze opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9e3a3-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="9e3a3-159">Open een browser toohello webadres op dat u hebt vastgelegd voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="9e3a3-160">Bijvoorbeeld: *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="9e3a3-161">U ziet er ongeveer zo Hallo na pagina:</span><span class="sxs-lookup"><span data-stu-id="9e3a3-161">You should see something like hello following page:</span></span>

    ![Book record](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="9e3a3-163">Gegevens in de tekstvakken Hallo invoeren en op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="9e3a3-164">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9e3a3-164">For example:</span></span>

    ![Book record toevoegen](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="9e3a3-166">Na het Hallo-pagina te vernieuwen, ziet u dat lijkt op deze pagina:</span><span class="sxs-lookup"><span data-stu-id="9e3a3-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Lijst adresboekrecords](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="9e3a3-168">U kunt klikken **verwijderen** en Hallo book record verwijderen uit Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e3a3-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e3a3-169">Next steps</span></span>

<span data-ttu-id="9e3a3-170">In deze zelfstudie maakt u een webtoepassing waarin wordt bijgehouden adresboek registreert met behulp van een gemiddelde gemaakt stack op een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="9e3a3-171">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="9e3a3-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e3a3-172">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="9e3a3-172">Create a Linux VM</span></span>
> * <span data-ttu-id="9e3a3-173">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="9e3a3-173">Install Node.js</span></span>
> * <span data-ttu-id="9e3a3-174">MongoDB installeren en het Hallo-server instellen</span><span class="sxs-lookup"><span data-stu-id="9e3a3-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="9e3a3-175">Express installeren en routes toohello server instellen</span><span class="sxs-lookup"><span data-stu-id="9e3a3-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="9e3a3-176">Toegang Hallo routes met AngularJS</span><span class="sxs-lookup"><span data-stu-id="9e3a3-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="9e3a3-177">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9e3a3-177">Run hello application</span></span>

<span data-ttu-id="9e3a3-178">Hoe gaan van de volgende zelfstudie toolearn toohello toosecure webservers met SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="9e3a3-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e3a3-179">Webserver met SSL beveiligde</span><span class="sxs-lookup"><span data-stu-id="9e3a3-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
