### Configurando o travis 

Devemos criar um arquivo chamado .travis.yml dentro do nosso repositório 

###
sudo: required #ativa as permissões de sudo para fazer o build 
services: #garante que o travis instalae o docke
  - docker

before_install: #passos para serem executados antes de executar a tarefa principal
  - docker build -t jorgejsilva/docker-react -f Dokerfile.dev .  #faz p build da imagem de desenvolvimento

#contém os comandos necessários para executar o teste
script:
  - docker run -e CI=true USERNAME/docker-react npm run test