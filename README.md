# Pipeline DevSecOps - Landing Page

Fluxo: commit -> Build -> Sonar -> Trivy -> Push (Docker Hub) -> Deploy (kind)

## Estrutura
Coloque os arquivos da landing page (index.html, css, js, imagens) na RAIZ do repositorio,
junto com estes arquivos.

## Configuracao unica
1. Secrets (Settings > Secrets and variables > Actions):
   DOCKERHUB_USERNAME, DOCKERHUB_TOKEN, SONAR_TOKEN
2. SonarCloud: importar o repo e ajustar projectKey/organization no sonar-project.properties.
   Em SonarCloud: desativar "Automatic Analysis" (Administration > Analysis Method).
3. k8s/deployment.yaml: trocar SEU_USUARIO_DOCKERHUB pelo usuario do Docker Hub.
4. Docker Hub: deixar o repositorio landing-page publico (o kind precisa baixar a imagem).
5. Runner self-hosted (Settings > Actions > Runners > New self-hosted runner) na maquina com kind e kubectl.

## Cluster
kind create cluster --name devops --config kind-config.yaml
Frontend: http://localhost:8080

## Apresentacao
- Aba Actions com a pipeline verde
- Resumo do job Trivy e artefato relatorios-trivy
- Dashboard no SonarCloud
- Frontend em localhost:8080
- Faca um commit ao vivo e recarregue a pagina
