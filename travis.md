```` YAML
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

##Fazendo deploy no elasticbeanstalk
deploy:
  provider: elasticbeanstalk
  region: "us-east-2"  #inserir a região onde o elasticbeanstalk foi criado.
  app: docker #node dadado na hora da criação do elasticbenastalk 
  env: "Docker-env" #nome do environment criado pelos elasticbeanstalk
  bucket_name: "elasticbeanstalk-us-east-2-494106798208" #nome do s3 bucket criado para o projeto
  bucket_path: "docker" #path no bucket para fazer o deploy do projeto. Utilizar o mesmo valor difinido em app:
  on: #só faz o deploy quando existir um commit na branch master
    branch: master

