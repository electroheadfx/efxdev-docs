# Remix with Fly

## Needed Tools

1. [Install Git](https://github.com/git-guides/install-git)

2. [Install GitHub CLI](https://cli.github.com)

3. [Install Fly CLI](https://fly.io/docs/flyctl/installing) :

```bash
$ brew install flyctl # on mac, see Instal doc for others OS
# login to fly
$ fly auth signup
# List all fly accounts with whoami:
$ fly auth whoami
```

## Create remix app

```bash
# via remix stack on blues-stack template
# Taiwind + Docker + Postgres + Vitest + Cypress with CI/CD on Fly
$ npx create-remix --template remix-run/blues-stack <repo-name>
# or use efx/reapp
# it does a pnpm setup + Postgres docker mount/migration + Git setup
$ reapp.sh --remix <repo-name>
$ cd <repo-name>
```

## Create the github repository

```bash
# $ repo="my-repo" # setup repo
# $ read -p "Enter your repo name : " repo # or ask it

# test if its a remix app
$ [ ! -n $(grep "^@remix-run/react\$" package.json) ] && echo "No remix app" && exit
# auto get from current repo
$ repo=$(basename $(pwd))
# Login to gh
$ gh auth login
# <repository> is your github repository name in public
$ gh repo create "$repo" --public
# or in private :
$ gh repo create "$repo" --private
# repo url = https://github.com/<account>/<repository>.git
```

```bash
$ git init
# change master to main (prod)
$ git branch -m master main
# Add files
$ git add .
# Do the first commit
$ git commit -m "First Setup"
# create a dev branch for staging
$ git branch dev
# do not publish yet before to setup fly
# main branch is for fly prod server
# dev branch is for fly staging server
```

## Fly setup

```bash
# get authentified
$ fly auth signup
# Create fly servers (prod and staging)
$ fly create "$repo"
$ fly create "$repo"-staging

# Create secrets app
$ fly secrets set SESSION_SECRET=$(openssl rand -hex 32) --app "$repo"
$ fly secrets set SESSION_SECRET=$(openssl rand -hex 32) --app "$repo"-staging
$ fly secrets set ADMIN_EMAIL=laurent@efxdesign.fr

# Create Fly DBs
$ fly postgres create --name "$repo"-db
$ fly postgres create --name "$repo"-staging-db

# Attach dbs to servers
$ fly postgres attach --postgres-app "$repo"-db --app "$repo"
$ fly postgres attach --postgres-app "$repo"-staging-db --app "$repo"-staging
```

## Publish to Git for deploy in fly

- **Create** `FLY_API_TOKEN` from *Fly* : [Create New Fly Token](https://web.fly.io/user/personal_access_tokens/new)

- **Paste** the`FLY_API_TOKEN` in **Secrets>Actions>”new repository secret“** OR :

```bash
# auth to githun gh
$ gh auth login
# setup origin repo
$ git remote add origin "https://github.com/electroheadfx/${repo}.git"
# paste the key via cli $TOKEN
$ gh secret set FLY_API_TOKEN --body "$TOKEN"
# or paste via pasteboard
$ gh secret set FLY_API_TOKEN
```

- **Publish** the code, it will run the deploy action from Github, to **Fly** :

```bash
$ git push -u origin main
```

## How Delete an repo/app on git and fly

```bash
# Delete Github repository
# Get repo input
# login
$ gh auth login
# delete repo
$ gh repo delete "https://github.com/electroheadfx/${repo}.git"
# --confirm if you are sure

# Delete Fly apps server
$ fly apps list # see the fly apps
# destroy the prod/staging servers
$ fly destroy "$repo" && fly destroy "$repo"-staging
# destroy the prod/staging DBs servers
$ fly destroy "$repo"-db && fly destroy "$repo"-staging-db
```
