# github-actions-workflows

Simple github actions workflows for deploying PHP or HTML websites.

## !!!WARNING!!!

You will most likely need to update the workflow for each project. Backup your site before you deploy and always test in a non-production environment first.

## Production Deployment

**The `production.yml` workflow contains instructions for the following:**
- clone the repository
- install PHP dependancies via Composer
- install npm package
- build assets with Laravel Mix
- deploy the site files to the production environment via rsync

**It does not contain instructions for the following:**
- Database migration
- Backups prior to deployment

## Configuration

To use with an existing repository create a directory titled `.github/` in the project root. Copy the `workflows/` directory from this repository to the `.github/` directory you created. You will likely need to update the workflow provided for each project but it should get you started.

**Workflow Triggers:**

- Manually via workflow dispatch (either through the GUI or gh cli command)
- Automatically via merge to main branch

**Github Secrets:**

You must add all your secrets to Github prior to running the workflow or it will fail.

- `SSH_HOST`: The host that github will connect to.
- `SSH_PRIVATE_KEY`: The private key that github will use to connect to your server. The public key needs to be added to server.
- `SSH_USER`: SSH user that github will use to connect to your server.
- `SSH_PATH`: The absolute path to the document root.
- `SLACK_WEBHOOK`: The slack webhook to deliver success/failure messages to.

**.rsyncignore**
This file is used to tell rsync which files to ignore. It prevents deployment of files, and protects them on the destination server. The following are just examples, not exhaustive lists. See the `.rsyncignore` file for more examples.

Examples of files you don't want to deploy:
- `/.git/`
- `/.github/`
- `/node_modules/`

Examples of files you need to protect on the destination server:
- `.env` or `.env.php`
- `/public/uploads/`
- `/public/.htaccess`

**Actions Used:**
- [rtCamp/action-slack-notify@v2](https://github.com/rtCamp/action-slack-notify)
- [actions/checkout@v4](https://github.com/actions/checkout)
- [php-actions/composer@v6](https://github.com/php-actions/composer)
- [actions/setup-node@v4](https://github.com/actions/setup-node)
- [webfactory/ssh-agent@v0.5.3](https://github.com/webfactory/ssh-agent)
