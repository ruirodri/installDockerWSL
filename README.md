# installDockerWSL
Guia para a instalação do Docker Engine sob WSL no Windows 10.


#Comando que mostra o status atual do WSL
wsl --status

#comando que mostra as distribuições instaladas no seu computador
wsl --list

#Comando que lista todas as distribuições de wsl disponíveis online
wsl --list --online

#Define que vamos trabalhar por padrão com o WSL versão 2.
wsl --set-default-version 2

#Vamos instalar um Linux Ubuntu versão 20.04
wsl --install -d Ubuntu-20.04

#Buscar a lista de atualizações para o SO
sudo apt update

#Fazer a atualização do SO
sudo apt upgrade

#Ao final da atualização, fechar a janela do terminal Linux

#Na janela de terminal do windows, 
wsl --shutdown

#No menu iniciar, procurar por "Ubuntu" e iniciar o Ubuntu 20.04 que aparecerá.

#Já estamos com o Linux instalado e atualizado. Agora, vamos começar a instalação do Docker propriamente dito.

#Instalando pré-condições para a instalação do Docker
sudo apt install --no-install-recommends apt-transport-https ca-certificates curl gnupg2

#Carregando em variáveis de ambiente definições da distribuição e versão 
source /etc/os-release

#Adicionando um repositório de pacotes como origem de instalação
curl -fsSL https://download.docker.com/linux/${ID}/gpg | sudo apt-key add -
echo "deb [arch=amd64] https://download.docker.com/linux/${ID} ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/docker.list

#Buscando a lista de pacotes deste novo repositório adicionado
sudo apt update

#Instalando os pacotes do Docker Engine
sudo apt install docker-ce docker-ce-cli containerd.io

#Baixando o binário do Docker Compose diretamente do GitHub
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

#Tornando o binário do Docker Compose executável
sudo chmod +x /usr/local/bin/docker-compose

#Executando o daemon do docker
sudo dockerd

#Baixando a imagem do Redmine e executando como exemplo
sudo docker run --rm -d -p 80:3000 --name meuRedmine redmine

