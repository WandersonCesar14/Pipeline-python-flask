Tutorial Jenkins: Configuração de Pipeline para Projeto Python Flask 

Passo 1: Permissões Necessárias

1.1. Acesse o diretório necessário:

cd /var/run
1.2. Conceda permissões ao docker.sock:

sudo chmod 777 docker.sock
1.3. Adicione um novo usuário chamado jenkins:

sudo useradd jenkins
1.4. Adicione o usuário jenkins ao grupo docker:

sudo usermod -aG docker jenkins
1.5. Verifique se o usuário jenkins foi adicionado ao grupo docker:

grep docker /etc/group
Passo 2: Criando a Pipeline no Jenkins

2.1. Faça login no Jenkins.

2.2. Clique em + Novo Tarefa.

2.3. Insira o nome da pipeline, selecione pipeline, e clique em Tudo certo.

2.4. Insira uma descrição (opcional).

2.5. Vá para a seção Pipeline.

2.6. Em Definition, clique em Pipeline script e selecione Pipeline script from SCM.

2.7. Em SCM, escolha Git.

2.8. No campo Repository URL, insira a URL do projeto no github

2.9. Configuração da pipeline, adicione o arquivo Jenkinsfile no seu projeto do github com esse script abaixo.

pipeline {
    agent { docker { image 'python:3.7.2' } }
    stages {
        stage('build') {
            steps {
                sh 'bash -c pip install flask'
            }
        }
        stage('test') {
            steps {
                sh 'bash -c python3 test.py'
            }
        }
    }
}


2.10. Em Branch Specifier, insira o nome da branch, que neste caso é */main.

2.11. Clique em Salvar para finalizar a configuração da pipeline.

Passo 3: Executando a Pipeline

3.3. Após criar a pipeline, no lado direito, clique em Construir agora.

3.2. Em seguida, clique em Open Blue Ocean para gerenciar a pipeline com uma interface gráfica.

3.3. Certifique-se de que a pipeline foi configurada corretamente e inicie a execução.


Com estas orientações suplementares, a sua pipeline Jenkins está agora completamente preparada para gerenciar o seu projeto de forma eficiente. Siga os passos para automação contínua.

