# The Hive & Cortex

### Deployment

Elastic & Cassandra both need increased vm.max_map_count so on the host machine need to do:

```
sysctl -w vm.max_map_count=1048575
```

Clone the repository

```bash
git clone https://github.com/razuz/th2

```

And cd into the correct directory:

```
cd th2/11-hive
```

Run docker compose:

```
docker compose up -d
```

> [!NOTE]
> This docker compose file uses Let's Encrypt certificates with the http challenge i.e. public IP-s are required

# Initial configuration

After containers have been created & are running

1. Navigate to cortex web ui and click update dabase. After the database setup is completed you can configure the first admin user
2. With the default admin, log in and create your organisation
3. Under the new organisation create an admin user and generate an API key for it (could also keep admin separate and create a second account with API key for Hive)
4. Log in to The Hive with the default credentials of username `admin@thehive.local` & password `secret`
5. Create an organisation and your users into that organisation
6. From the left hand side navigate to platform management and then click on the Cortex tab.
7. In this tab you can either configure the default cortex instance connection details with your API key or create a new server configuration
