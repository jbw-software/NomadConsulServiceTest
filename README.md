# NomadConsulServiceTest
POC running a simple service with HashiCorp Nomad, registering it with Consul and routing with Spring Cloud Gateway.

Using this [guide](https://medium.com/hashicorp-engineering/hashicorp-nomad-from-zero-to-wow-1615345aa539) for using a simple http-echo with Nomad and Consul.

### Prerequisites:
1. Install Docker on macOS using brew  
  brew install docker --cask
2. Install Nomad on macOS using brew  
  brew tap hashicorp/tap  
  brew install hashicorp/tap/nomad
3. Install JDK19 e.g. GraalVM using SDKMAN!  
  sdk list java  
  sdk install java 22.3.r19-grl

### Run
1. Run Nomad  
  nomad agent -dev
2. Open Nomad WebUI  
  http://localhost:4646/ui/jobs
3. Upload, plan and run Consul  
  use "consul.hcl"
4. Upload, plan and run http-echo  
  use "http-echo.hcl"
5. Install and run api-gateway  
  ./mvnw clean install && java -jar ./target/api-gateway-0.0.1-SNAPSHOT.jar 
7. List services in Consul WebUI  
  http://127.0.0.1:8500/ui/dc1/services
8. Open service WebUI through the api-gateway  
  http://127.0.0.1:8765/http-echo
  
### Try out
1. List allocated tasks  
  nomad job allocs http-echo-dynamic-service
2. Kill single task  
  nomad alloc stop [ALLOCATION_ID]
3. Keep using service WebUI through the api-gateway  
  http://127.0.0.1:8765/http-echo
