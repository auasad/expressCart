# expressCart

## Installation

1. clone the project `git@github.com:auasad/expressCart.git`
3. Enter folder: `cd expressCart`
4. Install dependencies: `npm install`
5. Start application: `npm start --production`
6. Visit [http://127.0.0.1:1111](http://127.0.0.1:1111) in your browser

### Docker Setup 

The easiest way to get up and running is using Docker. Once the Docker CLI is installed from [https://www.docker.com/get-docker](https://www.docker.com/get-docker).

1. clone the project by typing the commadn 'git clone git@github.com:auasad/expressCart.git'
2. Run mongodb container with name expressdb : `docker run --name expressdb -d mongo`
3. Change `vim /config/settings.json` - `"databaseConnectionString": "mongodb://mongodb:27017/expresscart"`
5. Run: `docker run -p 8080:1111 -d --name expresscart-app --link expressdb:mongodb auasad/expresscart` ## will run the container from the image created by Dockerfile with name auasad/expresscart
6. Visit [http://127.0.0.1:8080](http://127.0.0.1:8080) in your browser

### Docker-compose

1. Enter the root of the expressCart application
2. Change `/config/settings.json` - `"databaseConnectionString": "mongodb://mongodb:27017/expresscart"`
3. Run: `docker-compose up --build`
4. Visit [http://127.0.0.1:1111](http://127.0.0.1:1111) in your browser

## Admin

Visit: [http://127.0.0.1:1111/admin](http://127.0.0.1:1111/admin)


For more settings please switch to master branch.

