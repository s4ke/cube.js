# Building a metrics dashboard with Superset and Cube

Please see the [blog post](https://cube.dev/blog/building-metrics-dashboard-with-superset/) for instructions.

# Get an environment

https://labs.play-with-docker.com

# Setting up the stack locally

Setup:

```bash
docker-compose up -d
```

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

Then, initialize the database...

```bash
docker exec -it superset superset db upgrade
```

...and setup roles:

```bash
docker exec -it superset superset init
```

That's it! Now you should be able to navigate to [localhost:8080](http://localhost:8080/login/) and log into your Superset instance using the username and password from above.

## Running Cube locally

The last part of configuration is the [data schema](https://cube.dev/docs/schema/getting-started) which declaratively describes the metrics we'll be putting on the dashboard. Actually, Cube can generate it for us!

Navigate to [localhost:4000](http://localhost:4000) and, on the Schema tab, select the "public" schema with all tables, and generate data schema files. Now, you should be able to see files like `LineItems.js`, `Orders.js`, `Users.js`, etc. under the "schema" folder.
