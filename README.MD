# Docker register

Abaixo está um exemplo de arquivo docker-compose.yml para configurar o Docker Registry localmente no seu servidor. Este exemplo assume que você deseja executar o Docker Registry na porta 5000 e persistir os dados do registro em um volume Docker.

### docker-compose.yml
```
version: '3'

services:
  registry:
    image: registry:2
    container_name: registry
    ports:
      - "5000:5000"
    restart: always
    volumes:
      - registry_data:/var/lib/registry

volumes:
  registry_data:
    driver: local
```

## Explicação do Arquivo docker-compose.yml:

Versão e Serviços:

version: '3': Define a versão do Docker Compose.
services: Bloco onde definimos nossos serviços.
Serviço registry:

image: registry:2: Usa a imagem oficial do Docker Registry na versão 2.
container_name: registry: Nome do contêiner.
ports: Mapeia a porta 5000 do contêiner para a porta 5000 do host.
restart: always: Garante que o contêiner seja reiniciado automaticamente em caso de falha.
volumes: Define um volume chamado registry_data para persistir os dados do registro.
Volumes:

registry_data: Define um volume Docker local chamado registry_data para armazenar os dados do registro.
Como Usar o Arquivo docker-compose.yml:
Salve o arquivo: Salve o conteúdo acima em um arquivo chamado docker-compose.yml.

Inicie o Docker Registry: No diretório onde você salvou o docker-compose.yml, execute o seguinte comando para iniciar o Docker Registry:

## bash
```
docker-compose up -d
```
O parâmetro -d executa o Docker Registry em segundo plano.

Verifique se o Docker Registry está em execução: Verifique se o contêiner do Docker Registry está em execução usando:

## bash
``` 
  docker ps
```
Você deve ver um contêiner chamado registry na lista.

## Uso do Registro Docker Local:

Para usar o registro Docker local, você precisará configurar suas imagens Docker para apontar para seu_endereco_ip:5000/nome-da-imagem.

## Faça o login no registro Docker local usando:

bash
```
docker login seu_endereco_ip:5000
```

Você será solicitado a fornecer um nome de usuário e senha. Por padrão, o registro Docker não requer autenticação, mas é recomendável configurar para ambientes de produção.

## Push e Pull de Imagens:

Para enviar uma imagem para o registro local:

bash
```
docker tag nome-da-imagem:tag seu_endereco_ip:5000/nome-da-imagem:tag
docker push seu_endereco_ip:5000/nome-da-imagem:tag
```
## Para puxar uma imagem do registro local:

bash
```
docker pull seu_endereco_ip:5000/nome-da-imagem:tag
```
