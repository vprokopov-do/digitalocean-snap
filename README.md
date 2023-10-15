## do-snap

DigitalOcean currently offers weekly automated backups for Droplets. However, you might want to back up your Droplets more frequently. `do-snap` is a serverless function that can be deployed on DigitalOcean to take periodic snapshots of a Droplet. It accepts the Droplet ID and a personal access token as input and uses a cron schedule as a trigger. By default, it runs every 6 hours, and you can adjust the frequency.


### Operational logic

`do-snap` connects to the DigitalOcean API and accesses your account using the provided personal access token. It takes a snapshot of the specified Droplet and deletes an old snapshot, ensuring that only a single snapshot copy is retained at all times.

### Prerequisites

To use `do-snap`, you'll need:
- The latest version of `doctl` with the serverless software [installed](https://docs.digitalocean.com/reference/doctl/reference/serverless/).
- A serverless namespace created and [connected](https://docs.digitalocean.com/products/functions/how-to/create-namespaces/) to `doctl`.
- A personal access token [generated](https://docs.digitalocean.com/reference/api/create-personal-access-token/) for using the DigitalOcean API.
- The Droplet ID or a list of comma-separated Droplet IDs that you want to back up. You can [retrieve](https://docs.digitalocean.com/products/droplets/how-to/retrieve-droplet-metadata/) the Droplet ID.


### How to deploy

1. Clone this GitHub repository to your local machine.
```
git clone https://github.com/vprokopov-do/do-snap
```
2. Modify `project.yml`:
- Replace the environment variable `token` with your personal access token. See the next section below for the `project.yml` example.
- Replace the environment variable `droplets` with your Droplet ID or list of comma-separated Droplet IDs.
- Optionally, rename a function and a trigger to names that make sense to you.
3. Rename the "your-droplet-name" directory to match your Droplet's name.
```
do-snap
├── project.yml
└── packages
    └── do-snap
        └── your-droplet-name
            └── snap.py
```
4. Optionally, modify `project.yaml` to adjust the cron schedule (it runs every 6 hours by default).
5. Use `doctl` to Deploy the Function on DigitalOcean.
```
doctl serverless deploy do-snap
```
Note that you need to run the deploy command on the entire cloned-down folder.

### Example `project.yml`
![Token](/images/example.png)

### Author
Vasily Prokopov [@vprokopov-do](https://github.com/vprokopov-do/)
