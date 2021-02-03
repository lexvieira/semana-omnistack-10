<h1 align="center">
    <img alt="DevRadar" title="#delicinha" src=".github/devradar.svg" width="250px" />
</h1>

<h4 align="center">
  🚀 Semana OmniStack 10.0
</h4>
<p align="center">
  <img alt="GitHub language count" src="https://img.shields.io/github/languages/count/Rocketseat/semana-omnistack-10">

  <img alt="Repository size" src="https://img.shields.io/github/repo-size/Rocketseat/semana-omnistack-10">
  
  <a href="https://github.com/Rocketseat/semana-omnistack-10/commits/master">
    <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/Rocketseat/semana-omnistack-10">
  </a>

  <a href="https://github.com/Rocketseat/semana-omnistack-10/issues">
    <img alt="Repository issues" src="https://img.shields.io/github/issues/Rocketseat/semana-omnistack-10">
  </a>

  <img alt="License" src="https://img.shields.io/badge/license-MIT-brightgreen">
</p>

<p align="center">
  <a href="#rocket-tecnologias">Tecnologias</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-projeto">Projeto</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-layout">Layout</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-como-contribuir">Como contribuir</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-licença">Licença</a>
</p>

<br>

<p align="center">
  <img alt="Frontend" src=".github/devradar.png" width="100%">
</p>

## :rocket: Tecnologias

Esse projeto foi desenvolvido com as seguintes tecnologias:

- [Node.js](https://nodejs.org/en/)
- [React](https://reactjs.org)
- [React Native](https://facebook.github.io/react-native/)
- [Expo](https://expo.io/)
- [Docker](https://www.docker.com/) - Nova Feature

## 💻 Projeto

O DevRadar é um projeto que visa conectar desenvolvedores próximos a você que trabalham com as mesmas tecnologias.

## 🔖 Layout

Você pode baixar o layout do projeto no formato `.sketch` através [desse link](.github/DevRadar.sketch).

Para abrir o arquivo no formato `.sketch` em qualquer sistema operacional utilize a ferramenta [Figma](https://figma.com).

## 🤔 Como contribuir

- Faça um fork desse repositório;
- Cria uma branch com a sua feature: `git checkout -b minha-feature`;
- Faça commit das suas alterações: `git commit -m 'feat: Minha nova feature'`;
- Faça push para a sua branch: `git push origin minha-feature`.

Depois que o merge da sua pull request for feito, você pode deletar a sua branch.

## :memo: Licença

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE.md) para mais detalhes.

---

Feito com ♥ by Rocketseat :wave: [Entre na nossa comunidade!](https://discordapp.com/invite/gCRAFhc)

---

# NodeJS, React and React Native rodando com Docker e Docker Compose. 
## Nova Contribuição by [Lexlima](https://github.com/lexvieira)
---

### Uma breve explicação sobre o que um Docker. 
Read this in other languages: [English](README.en.md), [Portuguese](README.md).

Imagine que você trabalhe ou apenas esteja estudando varias technologias diferentes, Meu caso, culpado!!! :) ou o de varios de nós que utilizam `NodeJS`, `React`, `C#`, `Ruby`, `PHP` ou mesmo `Haskell` (Estava testando poucos dias atrás \o/) ou por examplo você só queira rodar alguns comandos em linux no seu Note ou PC sem ter que instalar um [Virutal Box](https://www.virtualbox.org/) ou [VMWare](https://www.vmware.com/).Essas linguagens e suas IDEs *(integrated development environment)*  consomem recursos como HD, Memória, Processador e principalmente **tempo**. *

Portanto, temos o Docker para ter acesso a uma infinidade de imagens de diferentes plataformas, que podem ser instanciadas quando necessário e podem ser descartadas quando não mais necessárias. Para isso, a aplicação fica na sua máquina e é acessada através do container instanciado. 

Agora, mãos na massa.

1. Criar DockerFile.
2. Criar docker-compose.yml.

## [DockerFile](https://docs.docker.com/engine/reference/builder/) 

Para rodar o projeto será necessário executar o yarn install para cada um dos projectos, **backend, web e mobile**, abaixo estão os comandos básicos para trabalhar com Docker nesse projeto React. Nesse caso poderemos rodar os commandos diretamente dentro do container.

### DockerFile
```
  FROM node:12.14.1

  WORKDIR /opt/ui

  EXPOSE 3333 3000 19000 19001 19002 19006

  RUN apt-get update 

  RUN yarn global add expo-cli

  ENV PATH="$(yarn global bin):$PATH"

  USER 1000

  CMD ["node", "-v"]
```

Você pode dar um build da imagem usando o commando:
```
docker build -t omnistack10:v01 .
```

* **Rodar comandos dentro de cada projeto utilizando o \bin\bash**
> Você pode utilizar a mesma imagem para os 3 projetos, simplesmente mudando o -volume (-v) diretórios.

1. Backend 
``` 
docker run -ti -v $(pwd)/backend:/opt/ui omnistack10:v01 /bin/bash
```  

2. FrontEnd (web)
``` 
docker run -ti -v $(pwd)/web:/opt/ui omnistack10:v01 /bin/bash
```  

3. Mobile
``` 
docker run -ti -v $(pwd)/mobile:/opt/ui omnistack10:v01 /bin/bash
```  

* Dentro do container você pode rodar os commandos para atualização do projeto ou adicionar novas bibliotecas ao seu projeto normalmente.

Example:
```
docker run -ti -v $(pwd)/backend:/opt/ui omnistack10:v01 /bin/bash
node@a436c9b17a76:/opt/ui$ yarn install
yarn install v1.21.1
[1/4] Resolving packages...
[2/4] Fetching packages...
[#########----------------------------------------------------] 148/1404
Done in 4.45s.
``` 

Depois de atualizar os projetos rodando os comandos dentro do container, você pode colocar os serviços **backend, web, mobile** para rodar.

1. Rodar servidor NodeJS *(Run Server NodeJs)*
```
docker run -ti -v $(pwd)/backend:/opt/ui -p 81:3333 omnistack10:v01 yarn dev
```
1. Rodar Web Server React *(Run Server React*
```
docker run -ti -v $(pwd)/web:/opt/ui -p 80:3000 omnistack10:v01 yarn start
```

3. Rodar Serviço React Native Expo.
   > Usando o Docker Expo Developer Tools para emular o mobile app Android ou IOS, no caso do React Native. Este docker não será utilizado em produção.
  - Para podermos rodar a aplicação no celular e usar o *Expo Developer Tools* em nosso navegador temos que adicionar algumas configurações extras que poderiam estar em nosso *DockerFile*, porem teriamos maiores problemas para altera-lo tendo que fazer o rebuild toda vez que trocassemos de IP por exemplo.
  - Para lidar com isso, podemos usar o .env arquivo e adicionar as variáveis que precisamos acessar dentro do container.

**.env File**
``` 
REACT_NATIVE_PACKAGER_HOSTNAME=192.168.1.70
EXPO_DEBUG=true
EXPO_DEVTOOLS_LISTEN_ADDRESS=0.0.0.0
``` 

**Run Expo Developer Tools**
``` 
docker run -ti -p 19000:19000 -p 19001:19001 -p 19002:19002 -p 19006:19006 -v $(pwd)/mobile:/opt/ui --env-file .env omnistack:v01 yarn start  
```

## [docker-compose.yml](https://docs.docker.com/compose/)

OK, agora com os 3 docker containers rodando e funcionando temos que simplicar as coisas para não ter que ficar rodando varios comandos para subir as 3 instâncias, logo temos o **docker-compose.yml**. Um unico arquivo com a nossa estrutura inteira rodando.

### Our docker-compose.yml

```
  version: "3.5"
  services: 
    backend:
      container_name: backend_1
      build: 
        context: .
        dockerfile: Dockerfile
      ports: 
        - 81:3333
      volumes: 
        - ${PWD}/backend:/opt/ui
      command: yarn dev
    frontend:
      container_name: frontend_1
      build: 
        context: .
        dockerfile: Dockerfile
      ports:
        - 80:3000
      volumes: 
        - ${PWD}/web:/opt/ui
      command: yarn start
    expo:
      container_name: expo-android_1
      build: 
        context: .
        dockerfile: Dockerfile
      env_file: .env
      ports: 
        - 19000:19000
        - 19001:19001
        - 19002:19002
        - 19006:19006
      volumes:
        - ${PWD}/mobile:/opt/ui
      command: yarn start
```

Nesse caso utilizamos o mesmo **Dockerfile** para as 3 instâncias, uma vez que estamos utilizando **nodeJS** como nossa imagem padrão que já vem com *npm* e *yarn* por padrão é tranquilo utilizar somente um Dockerfile ou imagem local|dockerhub.

Examplo docker-compose.yml usando uma imagem local.
```
version: "3.5"
services: 
  backend:
    container_name: backend
    image: "omnistack10:v01"
    ports: 
      - 81:3333
    volumes: 
      - ${PWD}/backend:/opt/ui
    command: yarn dev
  frontend:
    container_name: frontend
    image: "omnistack10:v01"
    ports:
      - 80:3000
    volumes: 
      - ${PWD}/web:/opt/ui
    command: yarn start
```

### Building e rodando o docker-compose

```
docker-compose up --build -d

 ---> Using cache
 ---> 072396844407
Successfully built 072396844407
Successfully tagged semana-omnistack-10_backend:lates
....

 ---> Using cache
 ---> 072396844407
Successfully built 072396844407
Successfully tagged semana-omnistack-10_frontend:latest
....
 ---> Using cache
 ---> 072396844407
Successfully built 072396844407
Successfully tagged semana-omnistack-10_expo:latest
```

>--build - Build images before starting containers.
> -d, --detach - Detached mode: Run containers in the background,

depois somente. 

```
docker-compose up
```

Finalmente.

Com certeza, depois de criar as imagens utilizando o **docker-compose --build** você precisará rodar novos commandos, adicionar novos pacotes em sua aplicação, então você pode rodar os commandos dentro do docker acessando o *bash* com o *docker run*, mas agora com os novos nomes.

```
docker run -ti -v $(pwd)/backend:/opt/ui semana-omnistack-10_backend:latest /bin/bash

docker run -ti -v $(pwd)/web:/opt/ui semana-omnistack-10_frontend:latest /bin/bash

docker run -ti -v $(pwd)/mobile:/opt/ui semana-omnistack-10_expo:latest /bin/bash

➜  semana-omnistack-10 git:(run_on_docker) ✗ docker run -ti -v $(pwd)/backend:/opt/ui semana-omnistack-10_backend:latest /bin/bash
node@0167da3e3efe:/opt/ui$ ls
node_modules  package.json  src  yarn.lock
node@0167da3e3efe:/opt/ui$ cd src 
node@0167da3e3efe:/opt/ui/src$ ls
controllers  index.js  models  routes.js  utils  websocket.js
```

## Alias *(Bonus)*

Antes você estava rodando os comandos diretamente dentro do container, acessando o mesmo através do **docker run**.

Agora você ira usar o **alias** para rodar commandos dentro do container sem necessariamente acessa-lo.

Alias ou (apelidos) no Linux ou Windows(próximo update) é um jeito mais facil de você simplificar seus comandos criando atalhos para eles.

Você pode criar um alias apenas usando o terminal, porém é recomendado utilizar no linux seu arquivo **.bashrc | .zshrc** dentro da pasta **home do usuário**, dependendo do seu **Unix shell**.

Nesse caso vamos criar um **Alias** para o nosso **backend**, rodando os comandos dentro da pasta root da nossa aplicação (Importante) **(semana-omnistack-10)**.

Nosso alias aqui será  `d_be` (docker backend)

```
➜  semana-omnistack-10 git:(run_on_docker) ✗ alias d_be='docker run --rm -v $(pwd)/backend:/opt/ui semana-omnistack-10_backend:latest '
``` 

Agora rodamos comandos dentro do nosso **backend container** usando apenas o alias **d_be** *(docker backend)* para executar os comandos, sem necessariamente ter que acessar nosso container usando o **bash linux** diretamente.

Por exemplo, rodando o commando `yarn install`.

```
➜  semana-omnistack-10 git:(run_on_docker) ✗ d_be yarn install
yarn install v1.21.1
[1/4] Resolving packages...
success Already up-to-date.
Done in 0.18s.
```

Ou **yarn add socket.io-client**

`d_be yarn add socket.io-client `

Resultado

```
➜  semana-omnistack-10 git:(run_on_docker) ✗ d_be yarn add socket.io-client 
yarn add v1.21.1
[1/4] Resolving packages...
[2/4] Fetching packages...
info fsevents@2.1.2: The platform "linux" is incompatible with this module.
info "fsevents@2.1.2" is an optional dependency and failed compatibility check. Excluding it from installation.
[3/4] Linking dependencies...
[4/4] Building fresh packages...
success Saved lockfile.
success Saved 2 new dependencies.
info Direct dependencies
└─ socket.io-client@3.1.0
info All dependencies
├─ engine.io-client@4.1.1
└─ socket.io-client@3.1.0
Done in 11.52s.
➜  semana-omnistack-10 git:(run_on_docker) ✗ 
```

Você também pode criar alias para outros commandos, como escutar portas no Linux por exemplo.

```
alias ListenPorts='sudo lsof -i -P -n | grep LISTEN'
```
[ListenPorts](imgs/listenports.png)
<img alt="Listen Ports Linux" src="imgs/listenports.png">

# CREDITOS

Como normalmente, na primeira vez temos uma serie de problemas para configurar um ambiente, e com Docker não foi diferente, então aqui vai os creditos para os camaradas que ajudaram um pouco com esse pequeno projeto com Docker. 

### Rocketseat

- [rocketseat-education-semana-omnistack-10](https://github.com/rocketseat-education/semana-omnistack-10)

### Docker

- [Running Expo/React Native in Docker - Haseeb Majid - Nov 1, 2018](https://hmajid2301.medium.com/running-expo-react-native-in-docker-ff9c4f2a4388)

- [Running React Native in Docker — Part 1/2 - Pavan Welihinda - Dec 9, 2019](https://medium.com/@pavan168/pavanwelihinda-running-react-native-in-docker-a0fe0b0c776e)

- [How to Run React Native Expo Web in a Docker Container - rockyourcode - 2020-10-20](https://www.rockyourcode.com/how-to-run-react-native-expo-web-in-a-docker-container/)

- [Metro bundler with Expo dockerized app is not working](https://stackoverflow.com/questions/59638451/metro-bundler-with-expo-dockerized-app-is-not-working)

- [Securing WebSocket API prevents use of Expo DevTools](https://github.com/expo/expo-cli/issues/1081)

- [MDBootstrap Angular Project with Dockers](https://github.com/lexvieira/mdbootstrapangular)

### Alias

- [Linux and Unix alias command tutorial with examples](https://shapeshed.com/unix-alias/)
- [How to set and save an alias in Windows Command Line using doskey](https://www.youtube.com/watch?v=E_6Lklnakew)
- [Your Must-Have PowerShell Aliases for Docker](https://blog.sixeyed.com/your-must-have-powershell-aliases-for-docker/)

### Readme Format and Other Stuff ;)

- [GitHub Cheat Sheet](https://github.com/tiimgreen/github-cheat-sheet/blob/master/README.md)
- [Get started with Docker Compose](https://docs.docker.com/compose/gettingstarted/)
- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
- [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax#headings)