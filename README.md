### do-snap

#### Description

Currently, DigitalOcean offers weekly automated backups for Droplets. However, you may want to back up your Droplets more often. `do-snap` is a serverless Function that can be deployed on DigitalOcean to take periodic Snapshots of your Droplet. It takes the Droplet ID and API token as input. It uses a cron schedule as a trigger. By default, it runs every 6 hours, and you can adjust the frequency if required. 

#### Operational logic

`do-snap` would connect to DigitalOcean's API endpoint and access your account by using the API token that you have provided. It would take a Snapshot of a Droplet and delete an old Snapshot so that only a single Snapshot is maintained at all times.

#### Prerequisites

- You'd need to have the latest doctl with the serverless plug-in installed
- You'd need to have an API token generated
- You'd need to get a Droplet ID for a Droplet that you want to get backed up

##### How to deploy

1. Make a local clone of this GitHub repository
2. Modify project.yaml and replace environment variables token and droplet
3. Modify project.yaml and rename a function with the name of your Droplet
4. Rename the "your-droplet-name" directory with the name of your Droplet
5. Optional - modify project.yaml and adjust the cron schedule (runs every 6 hours by default)
6. Deploy a Function to DigitalOcean with doctl
