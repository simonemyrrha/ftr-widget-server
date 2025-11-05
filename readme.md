# Fundamentos Técnicos e Estratégicos / Docker & Docker Compose

- Necessário para as aulas 
    - Instalação do Docker desktop 
        - Windows[https://docs.docker.com/desktop/setup/install/windows-install/]  e [https://docs.docker.com/desktop/]
            Verifique se o seu sistema está com a virtualização ativada: [https://docs.docker.com/desktop/troubleshoot/topics/#virtualization]
            Caso você não tenha o WSL instalado ainda, não se preocupe, o instalador do próprio Docker também irá instalar ele.
            “Virtualization enabled in the BIOS” - Esse processo é diferente para cada marca de placa mãe, recomendamos a pesquisar pela sua fabricante.
            Faça o download do instalador na página: [https://docs.docker.com/desktop/install/windows-install/]. Tome cuidado para baixar a versão correta: x86_64 ou ARM
            Duplo clique em Docker Desktop Installer.exe para executar o instalador.
            Quando solicitado, certifique-se de que a opção "Use o WSL 2 em vez do Hyper-V" na página de Configuração está selecionada ou não, dependendo da sua escolha. (recomendamos usar WSL)
            Se o seu sistema suportar apenas uma das duas opções, você não poderá selecionar qual usar.
            Siga as instruções no assistente de instalação para autorizar o instalador e prosseguir com a instalação.
            Quando a instalação for bem-sucedida, selecione Fechar para completar o processo de instalação.
            Deve aparecer a solicitação para Aceitar os Termos para continuar. O Docker Desktop iniciará após você aceitar os termos.
            Observe que o Docker Desktop não será executado se você não concordar com os termos.


- Verificar quais as dependências para add no dockerfile
- Adicionar o arquivo Dockerfile
- Pegar uma imagem no hub.docker.com -> pega o nome : a versão -> nome:versão
- comandos docker
- docker build -t widget-server:v1 . (nome da sua escolha)
- docker image ls (lista de imagem - docker )
- docker run -p 3000:3333 widget-server:v1 

- docker run -p 3000:3333 -d widget-server:v1 -> rodar modo de teste para não travar o container

- docker ps (mostra os containers rodando)

- docker logs ID_container ( para visualizar os logs do docker)

- docker stop ID_container (para a aplicação)
- docker start ID_container (reiniciar a aplicação)
- docker container ls (lista o container rodando)

- docker ps -a ( mostra as aplicações rodadas)

- docker history mostra as camadas da imagem 

- Multistage Build

#
FROM node:20.18 AS base

RUN npm i -g pnpm

FROM base AS dependencies

WORKDIR /usr/src/app

COPY package.json pnpm-lock.yaml ./

RUN pnpm install

FROM base AS build

WORKDIR /usr/src/app

COPY . .
COPY --from=dependencies /usr/src/app/node_modules ./node_modules

RUN pnpm build
RUN pnpm prune --prod

FROM node:20.18-alpine AS deploy

WORKDIR /usr/src/app

COPY --from=build /usr/src/app/dist ./dist
COPY --from=build /usr/src/app/node_modules ./node_modules
COPY --from=build /usr/src/app/package.json ./package.json

ENV CLOUDFLARE_ACCESS_KEY_ID="#"
ENV CLOUDFLARE_SECRET_ACCESS_KEY="#"
ENV CLOUDFLARE_BUCKET="#"
ENV CLOUDFLARE_ACCOUNT_ID="#"
ENV CLOUDFLARE_PUBLIC_URL="http://localhost"

EXPOSE 3333

CMD [ "node", "dist/main.mjs" ]
#

- Para mostrar a vulnerabilidade da image do container usamos o trivy
- pode ser instalado usando choco install trivy
- O banco de dados de vulnerabilidade [https://www.cve.org/]


FROM node:20-alpine3.21 AS deploy


- Distroless - Exploramos como usar imagens do Google Container Tools [https://github.com/GoogleContainerTools/distroless] e Chain Guard [https://images.chainguard.dev/directory/image/node/versions], destacando a importância de especificar corretamente os repositórios. Também discutimos a segurança e a eficiência das imagens, mostrando como elas podem ser mais leves e com menos vulnerabilidades. Por fim, abordamos a preparação para enviar essas imagens para repositórios online nas próximas aulas.