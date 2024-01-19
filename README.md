# MOD Traccar 2ECOMP

## Instalação Release

- Obtenha a instalação da versão 4.13 do Traccar em seu repositório (https://github.com/traccar/traccar/releases/tag/v4.13).
- Instale conforme orientação da página do Traccar.
- Apos instalação descompacte todo o conteúdo do arquivo release do MOD 2ECOMP na pasta onde foi instalado o Traccar.
- Inicie o Traccar

> Dica Instalação Traccar

```bash
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
sudo add-apt-repository 'deb [arch=amd64] http://mirror.zol.co.zw/mariadb/repo/10.3/ubuntu bionic main'
sudo apt install -y curl zip python software-properties-common bzip2 libio-socket-ssl-perl libnet-ssleay-perl unzip mariadb-server mariadb-client -qq
sudo apt remove --purge apache2 -y -qq
sudo apt autoremove -y -qq
sudo mysql_secure_installation
```

> Preparando banco de dados mysql
- Substitua NOVAESENHADEACESSO por uma senha de sua preferência e configure no traccar.xml o banco traccar, usuário traccar e a senha definida.
```bash
mysql -u root  -p  -e "create database traccar;"
mysql -u root  -p  -e "CREATE USER 'traccar'@'localhost' IDENTIFIED BY 'NOVAESENHADEACESSO';"
mysql -u root  -p  -e "GRANT ALL PRIVILEGES ON * . * TO 'traccar'@'localhost';"
mysql -u root  -p  -e "FLUSH PRIVILEGES;"

sudo systemctl restart traccar.service
```

> Caso o log dê erro de tamanho de BLOB inválido, configure o banco para que aceite tabelas INNODB do tipo Barracuda.
```bash
#mysql.ini
Editar my.cfg e adicionar no final do arquivo
innodb_file_per_table=1
innodb_file_format = Barracuda
```

## Instalação Shared Devices
> Core
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

- Copie e cole o conteudo abaixo no console e tecle enter
```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

- Instalando o node 16
```bash
nvm install 16
nvm use 16
```

> Web
```bash
cd shared/web
npm install -g serve
serve -p 3000
```

> Server
```bash
cd shared/server
apt install git -y
npm install
node index.js
```
