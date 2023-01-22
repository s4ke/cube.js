# Building a metrics dashboard with Superset and Cube

Please see the [blog post](https://cube.dev/blog/building-metrics-dashboard-with-superset/) for instructions.

# Get an environment

https://labs.play-with-docker.com

![grafik](https://user-images.githubusercontent.com/719760/213940741-65388c13-3d38-494f-a40f-6a89474f2550.png)

Create a node:

![grafik](https://user-images.githubusercontent.com/719760/213940796-96f94a91-f779-4f1c-9f74-9f349a3bf136.png)

# Clone the repository

```bash
git clone https://github.com/s4ke/cube.js.git
```

Next, we can go into the repository itself, the next commands will all happen there:

```bash
cd cube.js
```

Once done, your shell should look like this:

![grafik](https://user-images.githubusercontent.com/719760/213940905-de213246-6a95-4634-bbed-53b9289f1a5a.png)

# Install a terminal code editor

To do some editing later, we need an editor installed. We can simply install one

```bash
apk add nano
```

![grafik](https://user-images.githubusercontent.com/719760/213940982-8d5dfeab-7edd-4344-817d-51914251d99b.png)

# Setting up the stack locally

To setup, we simply run the following command in the terminal:

```bash
cd examples/cube.js
docker-compose up -d
```

Docker Compose will now setup all the necessary containers:

![grafik](https://user-images.githubusercontent.com/719760/213941071-101ccd7d-7d02-41da-80ff-0b80ec510cf9.png)

After a while you will notice that some services have been exposed via ports:

![grafik](https://user-images.githubusercontent.com/719760/213941103-6a62cffb-64f6-434f-b6f3-d2ffc0ffb3fe.png)

Under port 8080 we can find Superset:

![grafik](https://user-images.githubusercontent.com/719760/213941121-c1fef348-6176-4fc0-b7e1-2d1e5022b313.png)

Under Port 4000 we can find the cube.js playground:

![grafik](https://user-images.githubusercontent.com/719760/213941141-e2f9aa79-b705-414a-b525-accf5782ff6f.png)

## Investigate cube.js

cube.js allows us to explore the code for data cube that comes with this tutorial:

![grafik](https://user-images.githubusercontent.com/719760/213941237-8abe95c3-9f9d-465b-b6ef-5df2098a6ca4.png)

We can even explore data:

![grafik](https://user-images.githubusercontent.com/719760/213941189-67967d3d-11b3-4546-ba64-0110c1d0eea6.png)

Or create a dashboard app (this will take a while - we will not do this today):

![grafik](https://user-images.githubusercontent.com/719760/213943025-2231d4ea-555e-43e6-a802-b81bda22d03b.png)


## Setting up Superset locally

Setup an admin account. By default, the username and password would be set to `admin`, but you can definitely adjust the credentials as you wish:

```bash
docker exec -it superset superset fab create-admin \
  --firstname Superset \
  --lastname Admin \
  --email admin@superset.com \
  --username admin \
  --password admin
```

![grafik](https://user-images.githubusercontent.com/719760/213941487-64cef2a7-9e6c-4d21-9342-1f1e0fd3eb8f.png)


Then, initialize the database via migrations...

```bash
docker exec -it superset superset db upgrade
```

![grafik](https://user-images.githubusercontent.com/719760/213941526-a9462274-5928-4d48-9bd4-90ca96623109.png)

...and setup roles:

```bash
docker exec -it superset superset init
```

![grafik](https://user-images.githubusercontent.com/719760/213941577-bb1e9af7-baa4-4221-83a4-67af5b8a2046.png)

That's it! Now you should be able to navigate to superset and log into your Superset instance using the username and password from above (if you didn't change this, that's `admin` and `admin`.

## Setup Datasource on Superset

First, we go to the Database connections section of superset:

![grafik](https://user-images.githubusercontent.com/719760/213943285-a8c44c7e-e8bd-4cd7-b441-bff27acf2765.png)

Here we click on the button for a new database:

![grafik](https://user-images.githubusercontent.com/719760/213943302-4d0030cc-264e-4ac2-b84b-1fe82b9e99e6.png)

We select MySQL (cube.js emulates MySQL - in more modern versions this will be PostgreSQL, but for the sake of this tutorial this is fine):

![grafik](https://user-images.githubusercontent.com/719760/213317812-874f7d5b-a75d-40ae-9df1-b3dd07fe6381.png)

We have to enter the connection details:

```bash
Host: cube
Port: 3306
Database Name: ecom
Username: cube
Password: 12345
Display Name: cubejs
```

![grafik](https://user-images.githubusercontent.com/719760/213317751-1b44a98f-20d6-4d7f-bf3d-3ebb64261203.png)

We click on Finish and get: 

![grafik](https://user-images.githubusercontent.com/719760/213943415-8dbc7a69-5f78-4fad-ae13-1930a0b2e1a0.png)

We click finish here again. We have now successfully set up the database connection.

## Dashboards

We still have no BI dashboard yet. To start off, we can import the one from this repository.

For this we go to `Dashboards` and click the import button:

![grafik](https://user-images.githubusercontent.com/719760/213317918-40836b20-4da2-4ff9-a027-a176967f4f9f.png)

Next, we can select the dashboard we want to import.

![grafik](https://user-images.githubusercontent.com/719760/213943526-aa4ff3cb-f9ea-48cf-a789-258cf791365c.png)

For this lab, we use [the sample dashboard](./acme-dashboard.json)







