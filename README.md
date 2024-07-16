# Demo

Demo with NodeJS, Docker, Docker Compose, GitHub Actions, Jenkins, Ansible, Terraform, and AWS.

## Initialization

```bash
npm init -y
npm i express
npm i -D nodemon supertest jest
```

## Development

```bash
npm i
npm run dev
```

## Testing

```bash
npm run test
```

## Docker

To build and push a docker container for the app.

```bash
docker build -t <username>/demo .
echo $PASSWORD | docker login -u <username> --password-stdin
docker push <username>/demo --all-tags
```

## Docker Compose

Run the app with a mongo server using Docker Compose.

```bash
docker compose build --no-cache && docker compose up -d
```

## GitHub Action

- Action file at: `.github/workflows/action.yml`

- Tests run automatically on each push to the `main` branch that modifies files in the `app_nodejs` directory.
- Container build and push to DockerHub happens automatically once the tests pass.
  - Make sure to create repo secrets for `DOCKER_USERNAME` and `DOCKER_PASSWORD`

## Jenkins

- Run Jenkins server in docker.

  ```bash
  cd jenkins
  docker-compose up
  ```

- Install recommended plugins as well as `NodeJS` plugin.
- From Config Menu -> Tools -> Create NodeJS Installation named `node-22`
- Create a Pipeline for `app_nodejs` and a `Jenkinsfile` in the `app_nodejs` folder
- Connect the pipeline with GitHub Repository using the credentials plugin.
  - For automatic builds, setup SCM polling or Git hooks (available only when).
- Choose pipeline from SCM and configure the location of `Jenkinsfile`
- Trigger the build and monitor status (you may also install OpenSea plugin for a nicer UI).

## Terraform

Provision EC2 instance with the necessary configs to the run one instance of the web application.

```bash
nano ~/.aws/config # Update with your AWS connection config
```

```bash
cd terraform
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
```

## Ansible

Playbook to install Docker and run the app container on the provisioned instance.

```bash
cd ansible
ansible-galaxy collection install community.docker
ansible-playbook main.yml # make sure to update hosts.ini with the outputs from terraform
```
