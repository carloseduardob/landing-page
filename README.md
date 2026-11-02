# Pipeline DevSecOps - Landing Page

Pipeline no GitHub Actions que leva o codigo do commit ate o cluster kind:

commit -> 1 Build -> 2 Sonar -> 3 Trivy -> 4 Push (Docker Hub) -> 5 Deploy (kind)

## O que precisa ter no computador

- Windows 10/11 com WSL2 e virtualizacao ativada na BIOS
- Git
- GitHub CLI (gh)
- Docker Desktop (aberto e em execucao)
- kind
- kubectl
- Runner self-hosted do GitHub Actions (instalado e ligado)
- Minimo recomendado: 8 GB de RAM e 20 GB livres em disco


## Instalacao das ferramentas (Windows PowerShell)


Para instalar o que precisa (PowerShell como administrador):

    winget install -e --id Git.Git
    winget install -e --id GitHub.cli
    winget install -e --id Docker.DockerDesktop
    winget install -e --id Kubernetes.kind
    winget install -e --id Kubernetes.kubectl

Depois de instalar:

1. Reinicie o computador.
2. Abra o Docker Desktop e espere ficar "running" (aceite a instalacao do WSL2 se pedir).
3. Feche e abra o PowerShell.

Se o winget nao encontrar um pacote, use winget search NOME para ver o ID correto.
Em Linux ou macOS, instale as mesmas ferramentas com apt ou brew.


### Cluster kind

    kind create cluster --name devops --config kind-config.yaml
    kubectl get nodes

    kubectl apply -f k8s/
    kubectl rollout status deployment/landing-page

### 5. Runner self-hosted

O job de deploy roda na sua maquina, porque o kind e local.

No GitHub: repositório > Settings > Actions > Runners > New self-hosted runner (Windows x64).
Copie os comandos que a página mostra (download, config.cmd --url ... --token ...) e rode no PowerShell.
Deixe o .\run.cmd aberto.

Deixe esse terminal aberto: o runner precisa estar ligado para o deploy executar.

Quando terminar, confira o deploy:

    kubectl get pods
    kubectl get svc

E abra http://localhost:8080