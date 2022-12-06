Terraform Training

Vsevolod:

https://github.com/skabrits/Teraform-local


Program to defend.

https://12factor.net

Part I.
1. Setup local k3s from scratch with Vagrant
2. Implement HA k3s setup with Metal-LB on layer 2 (optionally plus FRR)
3. Document local k3s setup and networks
4. Deploy a django application (hello-world, which renders current tag / commit-id) to k3s cluster

Part II.
1. Use terraform to spin up a new VPC (virtual Private Cloud), Private network, EKS cluster
2. Store terraform state in S3 + use on-demand lock table in DynamoDB to apply changes
3. Implement github hooks to trigger:
    1. Helm chart build of Django app
    2. Push helm chart repository to AWS.
    3. Docker image build and upload to ECR
    4. Pushing helm chart to EKS to apps namespace

Part III.
1. Add observability (separate performance repository and performance namespace):
    1. Deploy Elasticsearch + Kibana helm chart to a separate logging namespace.
    2. Deploy Prometheus operator to track basic metrics (CPU/MEM) of deployed applications in the namespace apps. Deploy Grafana to performance namespace
    3. Deploy Jaeger to tracing namespace
2. Change application to support the devops tools:
    1. Make sure logs are always written to the console
    2. Add fluentbit side car to push logs from the application to Elasticsearch svc
    3. Add support for OpenTelemetry, add support for otel library, configure OTEL collector with jaeger (https://www.aspecto.io/blog/opentelemetry-collector-guide/), see for npm application

Part IV.
1. Create new Ops repository
3. Use ArgoCD or Flux to deploy the application whenever Ops repository is changed.