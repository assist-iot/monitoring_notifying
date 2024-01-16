
# Fping_DLT

  

Web service/API that provides a registry for endpoints (devices or gateways), performs crud operations on the registry, pings (Fping) the endpoints and sends unreachable endpoints to the specified DLT.

  
  

## Key Features

- Fping all endpoints (devices/gateways) in the registry

- Send unreachable endpoints to the specified DLT

- Get all endpoints (devices/gateways) in the registry

- Get all alive endpoints (devices/gateways) from the registry

- Get all unreachable endpoints (devices/gateways) from the registry

- Add new endpoint (device/gateway) to the registry

- Avoids duplicates (checks if the proposed endpoint already exists in the registry)

- Delete specified endpoint from the registry

- Checks if the proposed endpoint for deletion exists in the registry

- Perform add/delete endpoint operations from the command line interface

- Performs CRON job to automatically - in specified time intervals - ping (Fping) endpoints in the registry and post any unreachable endpoints to the DLT

  

## Prerequisites

- [Node.js](https://nodejs.org/en) (v18.14.0)

- [npm](https://www.npmjs.com/) / yarn packet manager

- [Fping](https://fping.org/) command line tool

- Install Fping

```bash

# sudo apt install fping [On Debian/Ubuntu]

```

  
  

## Installation

  

Use the package manager to install and start Fping_DLT.

  

- Install dependencies

```bash

//in the src folder

# npm install

```

- Start server in development mode

```bash

# npm run dev

```

- Start server in production mode

```bash

# npm start

```

  
  

## Configuration

  
  

- Default Port

- The app starts in port 5566 for both development and production mode

- The default port can be set in the ***config.js*** file

- Secondary port

- Uncomment line 36 in ***app.js*** - and set port number - to expose the app to another port (e.g. for monitoring etc).

```

// app.listen(6666, () => console.log(`server is listening at PORT: 6666`));

  

```

  
  
  

## Usage

  

- See [API documentation](https://documenter.getpostman.com/view/25916089/2s9YXh4MqF)

- **Add/Delete endpoint through CLI/CLI commands**

- Use the following commands providing the required feedback to the the terminal as prompted

  

```

//Command to add new endpoint

npm run endpoint:create

  

//Command to delete endpoint

npm run endpoint:delete

```

  

- **Cron job**

- Configure time intervals patterns in ***config.js*** as per requirements (see https://crontab.guru/ for details on usage)

- Stop cron by commenting out the following line in ***app.js*** file

  

```const { devicesJob, gatewaysJob } = require("./crons"); ```

- When enabled the folowing line appears in the terminal log at every trigger

  

```Device/Gateway cron triggered```

  

- ***Note**: The value of the "status" field of the endpoints in the registry is either "***alive***" or "***unreachable***" (see response of GET ***get all gateways/devices*** ) ie the status field has the same value ("unreachable") for both offline (unreachable) and not known (non existent) endpoints (urls). The difference between the two is visible in the responses of ***ping device/gateway - post alive***, as also documented below (see common errors) and only offline endpoints are posted to the DLT.

  
  

### **Error Handling**

- Common Errors

- Endpoint not known or unreachable, eg:

```

//terminal

  

//unreachable

EXEC command STDERR: ERROR: Error: Command failed: fping yahoo.gr

//not known

EXEC command STDERR: ERROR: Error: Command failed: fping klkj klkj;: Name or service not known

  

//postman

  

//unreachable

"Endpoint: \"b6bc9396-a9e7-48d7-ba14-9d297b1fac8b\" Command failed: fping yahoo.gr\n"

//not known

Command failed: fping adgadgadgagddag.com\nadgadgadgagddag.com: Name or service not known\n"

```

- Not connected to remote (DLT), eg:

```

//terminal

AXIOS ERROR for ID: "7c85871a-0609-4846-865b-0accf5f0e67e" connect ETIMEDOUT 10.10.10.2:31999

DLT UNREACHABLE - CHECK CONNECTION to DLT

  

//postman

Error: connect ETIMEDOUT 10.10.10.2:31999

```

  
  

## Contributing

  

Pull requests are welcome. For major changes, please open an issue first

to discuss what you would like to change.

  

Please make sure to update tests as appropriate.

  
  
  

**Contact Information:** ctsislianis@iti.gr# Fping_DLT
