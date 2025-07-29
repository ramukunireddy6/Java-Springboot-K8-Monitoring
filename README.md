Spring Boot Microservices Observability

This project contains a production-ready, Kubernetes-deployable architecture consisting of 7 Spring Boot microservices integrated with:

✅ Spring Security (ForgeRock JWT authentication)
✅ Centralized Logging using Log4j2 + Kafka
✅ Metrics collection via Prometheus
✅ Health checks with Spring Boot Actuator
✅ Visualization via Grafana dashboards
✅ Kubernetes deployment with readiness/liveness probes
🧱 Microservices Included

Microservice	        Description
auth-service	        Authenticates with ForgeRock (JWT)
gateway-service	API     Gateway using Spring Cloud Gateway
transaction-service	    Handles transaction records
account-service	        Validates and manages accounts
user-service	        (Optional) User profile/KYC
audit-service	        Consumes logs from Kafka for auditing
notification-service	Sends notifications on events
🚀 How to Run

🐳 Start Dependencies (Kafka, Prometheus, Grafana)
docker-compose -f docker-compose/kafka-zookeeper.yml up -d
docker-compose -f docker-compose/prometheus-grafana.yml up -d
☸ Deploy Microservices to Kubernetes
kubectl apply -f k8s/
Make sure Docker images for each service are built and accessible by your cluster (locally or via a registry).

🔍 Observability Stack

Prometheus scrapes /actuator/prometheus
Liveness/Readiness probes via /actuator/health/liveness & /readiness
Grafana Dashboards:
JVM metrics
Pod health
Transaction stats
Log4j2 → Kafka: All microservice logs go to topic app-logs
📊 Access Ports (Default)

Tool	URL
Prometheus	http://localhost:9090
Grafana	http://localhost:3000 (admin/admin)
Kafka UI	Use an external tool if desired
🧪 Post-Setup

Import Grafana dashboards from grafana/dashboards/
Monitor pod health, JVM memory, CPU usage
Consume logs from Kafka via CLI or log-consumer service
📁 Directory Structure

docker-compose/     → Kafka, Zookeeper, Prometheus, Grafana
k8s/                → Kubernetes YAMLs for all services
grafana/dashboards/ → JSON dashboards to import into Grafana
services/           → Source code layout for each microservice
📌 Requirements

Docker + Docker Compose
Kubernetes (minikube, k3s, EKS, etc.)
Maven or Gradle
JDK 17+
✅ To Do (Optional Enhancements)

Add CI/CD pipeline (e.g., GitHub Actions)
Add Helm charts for reusable deployments
Integrate distributed tracing (e.g., Sleuth + Zipkin)