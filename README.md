# Docker images for running terraform/terragrunt and iac utilities

## Build

```bash
docker build -t docker-terraform:tf-1.5.4-tg-0.48.5 -f terragrunt/Dockerfile .
docker build -t docker-terraform:tflint-0.47.0 -f tflint/Dockerfile .
```

## Run terraform

```bash
docker run --rm -v $(pwd):/work/ --workdir=/work/ -t docker-terraform:tf-1.5.4-tg-0.48.5 terraform init
docker run --rm -v $(pwd):/work/ --workdir=/work/ -t docker-terraform:tf-1.5.4-tg-0.48.5 terraform plan
docker run --rm -v $(pwd):/work/ --workdir=/work/ -t docker-terraform:tf-1.5.4-tg-0.48.5 terraform apply -auto-approve
docker run --rm -v $(pwd):/work/ --workdir=/work/ -t docker-terraform:tf-1.5.4-tg-0.48.5 terraform destroy -auto-approve
```

## Run terragrunt

```bash
docker run --rm -v $(pwd):/work/ --workdir=/work/ -t docker-terraform:tf-1.5.4-tg-0.48.5 terragrunt run-all plan
```

## Run tflint

```bash
docker run --rm -v $(pwd):/work/ --workdir=/work/ -t docker-terraform:tflint-0.47.0 tflint -f compact --recursive
```
