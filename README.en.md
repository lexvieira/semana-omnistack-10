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
- [Docker](https://www.docker.com/) - New Feature

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

# NodeJS, React and React Native running on Docker and Docker Compose. 
## Nova Contribuição by [Lexlima](https://github.com/lexvieira)
---

### A little explanation about Docker)
Read this in other languages: [English], 한국어, 日本語, 简体中文, 正體中文.

Imagine that you work or are just learning many different technologies, My case, Guilty!!! or the situation of many of us that use  `NodeJS`, `React`, `C#`, `Ruby`, `PHP` ou mesmo `Haskell` (I was using few days ago \o/ or for instance you just want to run some linux commands in your laptop or PC without need to install a  [Virutal Box](https://www.virtualbox.org/) ou [VMWare](https://www.vmware.com/)) Those languages and their IDEs (integrated development environment) consume resources like HD, Memory, Processor and mainly **time***

Therefore, we have Docker to have access to an infinite of images of different platforms, that can be instantiated when necessary and can be discarded when no longer needed. For this, the application is on your machine and is accessed through the instantiated container.

Agora, mãos na massa. Now, hands on.

1. Create DockerFile.
2. Create docker-compose.yml

## [DockerFile](https://docs.docker.com/engine/reference/builder/) 

To run the project will be needed execute the **yarn install** for each one of the projects, **backend, web e mobile**, below are the commands to work with Docker on that React project. In this case, we will run the commands directly from the container.

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

You can build the Docker image with the command:  
```
docker build -t omnistack10:v01 .
```

* **Execute commands inside of the container docker \bin\bash**.
> You can use the same builded image, basic change the -volumes directories.
 
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

* Inside the container, you can run all the commands normally, as update a project or add a new library.

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

After update the projects as you were updating in your own machine (actually it is, but using docker, save resources and just use when you need it), you can run the dockers for each app **backend, web, mobile***.

1. Rodar servidor NodeJS *(Run Server NodeJs)*
```
docker run -ti -v $(pwd)/backend:/opt/ui -p 81:3333 omnistack10:v01 yarn dev
```
1. Rodar Web Server React *(Run Server React*
```
docker run -ti -v $(pwd)/web:/opt/ui -p 80:3000 omnistack10:v01 yarn start
```

3. Run React Native Service Expo.
   > Once Docker Expo Developer Tools is to emulate the mobile app on Android or IOS, in the case of React Native. It will not be used in production).
  - To run the app on our smartphone or emulator and use the *Expo Developer Tools* in our browser we need to add some extra configurations que could be in our *DockerFile*, however it would be necessary to rebuild the Docker image everytime that we changed the Computer IP for instance.
  - To handle with this we can use the .env file to add the variables that we need to access inside of the container.

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

OK, now with 3 containers running we need to simplify the things for don't need to keep typing many commands. Therefore, we have **docker-compose.yml**. Only one file and our entire structure running.

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

In this case we used the same **Dockerfile** for the 3 instances, once that we are using **NodeJS** as our default image that already come with *npm* and *yarn* by default is simple use only one Dockerfile or image local|dockerhub.

Example docker-compose.yml using a localimage.
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

### Building and Running the docker-compose

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

after just. 

```
docker-compose up
```

Finally.

Sure, after create the images using **docker-compose --build** you will need to run new commands, add new packages in your application, so you can run the commands inside of docker accessing the **bash** using the **docker run**, but now with the new images names. 

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

Before you were running the commands inside the container, using the **docker run**.

Now you will see how to run the commands outside the container using the **alias**.

Alias on Linux or Windows (next update) are an easier way of you run commands creating shortcuts to them.

You can create an alias just using the terminal, although is recommended on Linux use your file **.bashrc | .zshrc** inside of the **home user folder**, depends on your **Unix shell**.

In this case we will create an **Alias** for our **backend**. running the commands inside the app root folder (Important) **(semana-omnistack-10)**.

Our alias here will be  `d_be` (docker backend)

```
➜  semana-omnistack-10 git:(run_on_docker) ✗ alias d_be='docker run --rm -v $(pwd)/backend:/opt/ui semana-omnistack-10_backend:latest '
``` 

Now we run commands inside our **backend container** using only the alias **d_be** *(docker backend)* to execute the commands, without necessarily need to access our container using the **bash linux** directly.

For instance, running the command `yarn install`.

```
➜  semana-omnistack-10 git:(run_on_docker) ✗ d_be yarn install
yarn install v1.21.1
[1/4] Resolving packages...
success Already up-to-date.
Done in 0.18s.
```

Or **yarn add socket.io-client**

`d_be yarn add socket.io-client `

Result

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

You also can create alias to other commands like listen linux ports.

```
alias ListenPorts='sudo lsof -i -P -n | grep LISTEN'
```
[ListenPorts](imgs/listenports.png)
<img alt="Listen Ports Linux" src="imgs/listenports.png">

# CREDITS

As normally at the first time we got a lot of problems to setup a environment, and with Docker it was not differente \o/, so here are the credits from the websites that help to finish this small project with Dockers.

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