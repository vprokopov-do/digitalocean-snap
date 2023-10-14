## do-snap

Currently, DigitalOcean offers weekly automated backups for Droplets. However, you may want to back up your Droplets more often. `do-snap` is a serverless Function that can be deployed on DigitalOcean to take periodic Snapshots of a Droplet. It accepts the Droplet ID and personal access token as input. And it uses a cron schedule as a trigger. By default, it runs every 6 hours, and you can adjust the frequency. 

### Operational logic

`do-snap` would connect to DigitalOcean API and access your account by using the personal access token provided. It would take a Snapshot of a Droplet you specify and delete an old Snapshot so that only a single Snapshot copy is kept at all times.

### Prerequisites

- You'd need the latest `doctl` with the serverless software [installed](https://docs.digitalocean.com/reference/doctl/reference/serverless/).
- You'd need to create a serverless namespace and [connect](https://docs.digitalocean.com/products/functions/how-to/create-namespaces/) `doctl` to it.
- You'd need to get a personal access token [generated](https://docs.digitalocean.com/reference/api/create-personal-access-token/) to use DigitalOcean API.
- You'd need to [obtain](https://docs.digitalocean.com/products/droplets/how-to/retrieve-droplet-metadata/) a Droplet ID of a Droplet that you want to get backed up.

### How to deploy

1. Make a local clone of this GitHub repository.
```
git clone https://github.com/vprokopov-do/do-snap
```
2. Modify `project.yml`:
- Replace the environment variable `token` with your personal access token. See the next section below for the `project.yml` example.
- Replace the environment variable `droplets` with your Droplet ID or list of comma-separated Droplet IDs.
- Optional – rename a function and a trigger to something that makes sense to you.
3. Rename the "your-droplet-name" directory to your Droplet's name.
```
do-snap
├── project.yml
└── packages
    └── do-snap
        └── your-droplet-name
            └── snap.py
```
4. Optional - modify `project.yaml` and adjust the cron schedule (runs every 6 hours by default).
5. Use `doctl` to Deploy the Function on DigitalOcean.
```
doctl serverless deploy do-snap
```
Note that you need to run the deploy command on the entire cloned-down folder.

### Example `project.yml`
![Token](/images/example.png)

### Author
Vasily Prokopov [@vprokopov-do](https://github.com/vprokopov-do/)
