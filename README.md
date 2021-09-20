# installDockerWSL
<b>Guia para a instalação do Docker Engine sob WSL no Windows 10.</b>


Comando que mostra o status atual do WSL<br />
<b>wsl --status</b>

Comando que mostra as distribuições instaladas no seu computador
<b>wsl --list</b>

Comando que lista todas as distribuições de wsl disponíveis online
<b>wsl --list --online</b>

Define que vamos trabalhar por padrão com o WSL versão 2.
<b>wsl --set-default-version 2</b>

Vamos instalar um Linux Ubuntu versão 20.04
<b>wsl --install -d Ubuntu-20.04</b>

<i>A partir daqui, os comandos vão para o terminal do Linux que se abre.</i>

Após a instalação, buscar a lista de atualizações para o SO
<b>sudo apt update</b>

Fazer a atualização do SO (pode demorar um pouco)
<b>sudo apt upgrade</b>

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

