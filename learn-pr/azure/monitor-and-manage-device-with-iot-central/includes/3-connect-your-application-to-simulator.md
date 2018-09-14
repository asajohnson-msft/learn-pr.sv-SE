I verkligheten förutsätts det att du ansluter Azure IoT Central till en verklig enhet eller i det här fallet en verklig kaffebryggare. Men i den här enheten du ansluta en Node.js-program, som representerar en fysisk/real kaffe dator till programmet Azure IoT Central. Till följd av den här anslutningen telemetri mått från den kaffe datorn skickas till IoT Central för övervakning och analys.

![Kaffebryggare](../images/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a>Lägg till kaffe-dator i IoT Central 
Om du vill lägga till datorn kaffe i ditt program du använder den **anslutna kaffe Maker** enheten mall som du skapade i den föregående enheten.

1. Om du vill lägga till en ny enhet, Välj **Device Explorer** i den vänstra navigeringsmenyn.

    För att ansluta datorn kaffe väljer **+ ny**, sedan **verkliga**. När du är klar kan se du en lista över enheter som du har skapat med hjälp av samma ansluten kaffe Maker-mallen.
   
    *   Den anslutna kaffe Maker läggs till i listan när du väljer + New och verkliga. 
    *   Ansluten kaffe Maker (simulera) skapas automatiskt av IoT Central för testning. 

1.  Alternativt kan du skilja den nyligen tillagda kaffe datorn genom att lägga till ordet ”verkliga” i namnet. Om du vill byta namn på den nya enheten, väljer enheten och redigera namnet i namnfältet på. 

    ![Kaffebryggare](../images/3-connect-device-a.png) 

    Anteckna platsen för **ansluta enheten** för att ansluta datorn kaffe i nästa avsnitt. För skärmen visar nu ”Data som saknas”, beror det på att du inte har anslutit till den kaffe-datorn. Riktig telemetri börjar att fylla skärmen när anslutningen görs. 
 
## <a name="get-connection-string-for-the-coffee-machine-from-your-application"></a>Hämta kaffebryggarens anslutningssträng från ditt program
Du bäddar in den verkliga kaffebryggarens anslutningssträng i den kod som körs på enheten. Anslutningssträngen gör att kaffebryggaren kan ansluta säkert till Azure IoT Central-programmet. Varje enhetsinstans har en unik anslutningssträng. Så här hittar du anslutningssträngen för en enhetsinstans i programmet:

1.  På skärmen enhet för dina anslutna kaffe datorn verkliga väljer **ansluta enheten**.

1.  På sidan **Anslut** kopierar du den **primära anslutningssträngen** och sparar den. Du använder det här värdet i klientprogrammet som körs på enheten.

## <a name="create-a-nodejs-application"></a>Skapa ett Node.js-program
Följande steg visar hur du skapar ett klientprogram som implementerar den kaffe datorn som du lade till programmet.
1. Installera [Node.js](https://nodejs.org/) version 4.0.x eller senare på din dator. Node.js är tillgängligt för många olika operativsystem.

1. Skapa en mapp med namnet kaffebryggare på datorn. Gå till den mappen i kommandoradsmiljön.

1. Initiera Node.js-projektet genom att köra följande kommandon:
    ```cmd/sh
    npm init
    ```
    > [!NOTE]
    > Skriptet init uppmanas du att ange Projektegenskaper för. För den här övningen är Använd standardvärden tillräcklig och rekommenderade. 
1. Kör följande kommando för att installera de nödvändiga paketen:
    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Skapa en fil med namnet coffeeMaker.js i mappen kaffebryggare med en textredigerare.

1. Kopiera och klistra in koden i filen coffeeMaker.js och **Spara**.

    Koden, som representerar den verkliga kaffe datorn i den här enheten, är skriven i Node.js. Du börjar genom att upprätta anslutningen med programmet och sedan du skicka inledande egenskaper till Azure IoT Central, synkronisera inställningarna, registrera dig två kommandot hanterare för underhåll och Brewing och slutligen starta timer för att skicka telemetri information om varje sekund.

    > [!NOTE]
    > Uppdatera platshållaren `{your device connection string}`. 


    ```js
    "use strict";

    // Use the Azure IoT device SDK for devices that connect to Azure IoT Central
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;

    // Connection string (TODO: CHANGE HERE)
    const connectionString = `{your device connection string}`;

    // Global variables
    var client = clientFromConnectionString(connectionString);
    var optimalTemperature = 96;
    var cupState = true;
    var brewingState = false;
    var cupTimer = 20;
    var brewingTimer = 0;
    var maintenanceState = false;
    var warrantyState = Math.random() < 0.5?0:1;

    // Helper function to produce nice numbers (##.#)
    function niceNumber(value) 
    {
        var number = (Math.round(value * 10.0)).toString();
        return number.substr(0, 2) + '.' + number.substr(2, 1);
    }

    // Send device simulated telemetry measurements
    function sendTelemetry() 
    {   
        // Simulate the telemetry values
        var temperature = optimalTemperature + (Math.random() * 4) - 2;
        var humidity = 20 + (Math.random() * 80);
        
        // Cup timer - every 20 second randomly decide if the cup is present or not
        cupTimer--;
        
        if (cupTimer == 0)
        {
            cupTimer = 20;
            cupState = Math.random() < 0.5?false:true;
        }
        
        // Brewing timer
        if (brewingTimer > 0)
        {
            brewingTimer--;
            
            // Finished brewing
            if (brewingTimer == 0)
            {
                brewingState = false;
            }
        }
    
        // Create the data JSON package
        var data = JSON.stringify(
        { 
            waterTemperature: temperature, 
            airHumidity: humidity, 
        });

        // Create the message with the above defined data
        var message = new Message(data);
        
        // Set the state flags
        message.properties.add('stateCupDetected', cupState);
        message.properties.add('stateBrewing', brewingState);
        
        // Show the information in console
        var infoTemperature = niceNumber(temperature);
        var infoHumidity = niceNumber(humidity);
        var infoCup = cupState ? 'Y' :'N';
        var infoBrewing = brewingState ? 'Y':'N';
        var infoMaintenance = maintenanceState ? 'Y':'N';
        
        console.log('Telemetry send: Temperature: ' + infoTemperature + 
                    ' Humidity: ' + infoHumidity + '%' + 
                    ' Cup Detected: ' + infoCup + 
                    ' Brewing: ' + infoBrewing + 
                    ' Maintenance Mode: ' + infoMaintenance);
        
        // Send the message
        client.sendEvent(message, function (errorMessage) 
        {
            // Error
            if (errorMessage) 
            {
                console.log('Failed to send message to Azure IoT Hub: ${err.toString()}');
            }
        });
    }

    // Send device properties
    function sendDeviceProperties(deviceTwin) 
    {
        var properties = 
        {
            propertyWarrantyExpired: warrantyState
        };
        
        console.log(' * Property - Warranty State: ' + warrantyState.toString());
        
        deviceTwin.properties.reported.update(properties, (errorMessage) => 
            console.log(` * Sent device properties ` + (errorMessage ? `Error: ${errorMessage.toString()}` : `(success)`)));
    }

    // Optimal temperature setting
    var settings = 
    {
        'setTemperature': (newValue, callback) => 
        {
            setTimeout(() => 
            {
                optimalTemperature = newValue;
                callback(optimalTemperature, 'completed');
            }, 1000);
        }
    };

    // Handle settings changes that come from Azure IoT Central via the device twin.
    function handleSettings(deviceTwin) 
    {
        deviceTwin.on('properties.desired', function (desiredChange) 
        {
            // Iterate all settings looking for the defined one
            for (let setting in desiredChange) 
            {
                // Setting we defined
                if (settings[setting]) 
                {
                    // Console info
                    console.log(` * Received setting: ${setting}: ${desiredChange[setting].value}`);
                    
                    // Update 
                    settings[setting](desiredChange[setting].value, (newValue, status, message) => 
                    {
                        var patch = 
                        {
                            [setting]: 
                            {
                                value: newValue,
                                status: status,
                                desiredVersion: desiredChange.$version,
                                message: message
                            }
                        }
                        deviceTwin.properties.reported.update(patch, (err) => console.log(` * Sent setting update for ${setting} ` +
                        (err ? `error: ${err.toString()}` : `(success)`)));
                    });
                }
            }
        });
    }

    // Maintenance mode command
    function onCommandMaintenance(request, response) 
    {
        // Display console info
        console.log(' * Maintenance command received');

        // Console warning
        if (maintenanceState)
        {
            console.log(' - Warning: The device is already in the maintenance mode.');
        }
        
        // Set state
        maintenanceState = true;

        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    function onCommandStartBrewing(request, response) 
    {
        // Display console info
        console.log(' * Brewing command received');

        // Console warning
        if (brewingState == true)
        {
            console.log(' - Warning: The device is already brewing.');
        }
        
        if (cupState == false)
        {
            console.log(' - Warning: The cup has not been detected.');
        }
        
        if (maintenanceState == true)
        {
            console.log(' - Warning: The device is in maintenance state.');
        }
        
        // Set state - brew for 30 seconds
        if ((cupState == true) && (brewingState == false) && (maintenanceState == false))
        {
            brewingState = true;
            brewingTimer = 30;
        }
        
        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    // Handle device connection to Azure IoT Central
    var connectCallback = (errorMessage) => 
    {
        // Connection error
        if (errorMessage) 
        {
            console.log(`Device could not connect to Azure IoT Central: ${errorMessage.toString()}`);
        } 
        // Successfully connected
        else 
        {
            // Notify the user
            console.log('Device successfully connected to Azure IoT Central');

            // Send telemetry measurements to Azure IoT Central every 1 second.
            setInterval(sendTelemetry, 1000);
            
            // Setup device command callbacks
            client.onDeviceMethod('cmdSetMaintenance', onCommandMaintenance);
            client.onDeviceMethod('cmdStartBrewing', onCommandStartBrewing);
            
            // Get device twin from Azure IoT Central
            client.getTwin((errorMessage, deviceTwin) => 
            {
                // Failed to retrieve device twin
                if (errorMessage) 
                {
                    console.log(`Error getting device twin: ${errorMessage.toString()}`);
                } 
                // Success
                else 
                {
                    // Notify the user
                    console.log('Device Twin successfully retrieved from Azure IoT Central');
                
                    // Send device properties once on device start up
                    sendDeviceProperties(deviceTwin);
                    
                    // Apply device settings and handle changes to device settings
                    handleSettings(deviceTwin);
                }
            });
        }
    };

    // Start the device (connect it to Azure IoT Central)
    client.open(connectCallback);



    ```

1.  Uppdatera platshållaren {enhetens anslutningssträng} med enhetens anslutningssträng. Du kopierade det här värdet från anslutningens informationssida när du lade till din verkliga enhet. 

## <a name="run-your-nodejs-application"></a>Kör Node.js-programmet
```cmd/sh
node coffeeMaker.js
```

## <a name="summary"></a>Sammanfattning
I den här enheten ansluten kaffe datorn till Azure IoT Central och började skicka data för övervakning och analys. Du har upprättat anslutningen genom att först skaffa en anslutningssträng från IoT Central och sedan konfigurera strängen i kaffebryggaren.