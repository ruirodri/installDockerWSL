# Guia para a instalação do Docker Engine sob WSL no Windows 10.
<br />

### Os comandos descritos são aplicados em um janela de command prompt (cmd), e você pode ir copiando as linhas em bold (que não estão iniciadas por "=>") e colando-as na janela de terminal
<br />

=> Comando que mostra o status atual do WSL <br /> **wsl --status**
<br />

=> Caso não tenhamos o WSL instalado, este guia da Microsoft conduz pelo passo a passo da instalação <br> https://docs.microsoft.com/pt-br/windows/wsl/install-win10
<br>

=> Comando que mostra as distribuições instaladas no seu computador <br /> **wsl --list**
<br />

=> Comando que lista todas as distribuições de wsl disponíveis online <br /> **wsl --list --online**
<br>

### Aqui começa o processo de instalação do Linux.  <br>
=> Comando que define que vamos trabalhar por padrão com o WSL versão 2.<br /> **wsl --set-default-version 2**
<br />

=> Vamos instalar um Linux Ubuntu versão 20.04 (demora um pouco!) <br /> **wsl --install -d Ubuntu-20.04**
<br />

#### A partir daqui, os comandos vão para o terminal do Linux que se abre. 
=> Após a instalação, buscar a lista de atualizações para o SO<br /> **sudo apt update**
<br />

=> Fazer a atualização do SO (vai demorar um pouco)<br /> **sudo apt upgrade**
<br />

=> Ao final da atualização, fechar a janela do terminal Linux<br />
=> Para forçar o restart do kernel Linux, na janela de terminal do windows digitar <br /> **wsl --shutdown**
<br />

### Aqui começa o processo de instalação do Docker dentro do Linux.  <br>
=> No menu iniciar, procurar por "Ubuntu" e iniciar o Ubuntu 20.04 que aparecerá.<br />
=> Abrirá novamente o terminal do Linux<br /><br />

=> Instalando algumas ferramentas que serão utilizadas no processo de instalação. <br /> **sudo apt install --no-install-recommends apt-transport-https ca-certificates curl gnupg2**
<br />

=> Carregando em variáveis de ambiente definições da distribuição e versão <br /> **source /etc/os-release**
<br />

=> Adicionando a chave GPG de um repositório de pacotes que usaremos como origem de instalação<br /> **curl -fsSL https://download.docker.com/linux/${ID}/gpg | sudo apt-key add -**

=> Adicionando o repositório em si à lista de origens de pacotes (atenção, comando pode aparecer aqui em mais de uma linha!)<br /> **echo "deb [arch=amd64] https://download.docker.com/linux/${ID} ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/docker.list**
<br />

=> Buscando a lista de pacotes deste novo repositório adicionado <br /> **sudo apt update**
<br />

=> Instalando os pacotes do Docker Engine<br /> **sudo apt install docker-ce docker-ce-cli containerd.io**
<br />

=> Baixando o binário do Docker Compose diretamente do GitHub (atenção de novo, comando longo!) <br /> **sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose**
<br />

=> Tornando o binário do Docker Compose executável <br /> **sudo chmod +x /usr/local/bin/docker-compose**
<br />

=> Executando o daemon do docker. <br /> **sudo dockerd**
<br />

=> Abrir outra janela de terminal do Linux (pelo menu do windows ou com botão direito no ícone da barra de tarefas)<br />
=> Para validar a instalação, vamos baixar a imagem do Redmine e executá-lo. <br /> **sudo docker run --rm -d -p 5080:3000 --name meuRedmine redmine**
<br />
<br />
=> Para acessar o container que acabamos de iniciar, abrir o browser e acessar "http://localhost:5080"<br />
=> O usuário padrão é "admin", com a senha "admin", e esta senha precisa ser alterada no primeiro acesso.<br /><br /><br />

=> Referências utilizadas: <br />
https://dev.to/bowmanjd/install-docker-on-windows-wsl-without-docker-desktop-34m9<br />
https://phoenixnap.com/kb/install-docker-compose-on-ubuntu-20-04
<br />
<br />
### Dica: não esqueça de fechar o daemon do Docker (usando Ctrl+C) antes de fechar o Linux



