r'''# Instalando o Java

Existem diferentes formas de instalar o Java, e cada uma pode ser mais conveniente dependendo do ambiente em que estamos trabalhando.

Decidi documentar três formas de instalação: uma para Windows e duas para Linux. No dia a dia, sou usuário de Linux, mas também utilizo Windows para alguns trabalhos, então considero útil saber preparar um ambiente Java nas duas plataformas.

Nas instalações abaixo, estou utilizando o Java 21, uma versão LTS (Long-Term Support).

---

# Windows

No Windows, podemos utilizar o próprio instalador do JDK da Oracle.

Essa é provavelmente a forma mais direta de instalar o Java no Windows. Por outro lado, é uma abordagem mais "engessada" quando comparada a ferramentas como o SDKMAN!, já que a instalação e a troca entre versões ficam mais manuais.

Ainda assim, ela é bastante funcional, principalmente em máquinas ou servidores onde precisamos apenas de uma versão específica do Java instalada.

## 1. Baixando e instalando o JDK

O instalador pode ser obtido diretamente no site oficial da Oracle:

https://www.oracle.com/java/technologies/downloads/#java21

Durante a instalação, precisamos prestar atenção ao diretório onde o JDK será instalado.

No meu caso, foi instalado em:

C:\Program Files\Java\jdk-21.0.12.1\

É importante anotar esse caminho, pois ele será utilizado posteriormente na configuração das variáveis de ambiente.

---

## 2. Configurando as variáveis de ambiente

Depois de instalar o JDK, precisamos configurar a variável de ambiente JAVA_HOME.

A JAVA_HOME deve apontar para a pasta onde o JDK foi instalado.

No meu caso:

JAVA_HOME=C:\Program Files\Java\jdk-21.0.12.1

Além disso, precisamos adicionar o diretório bin do JDK à variável Path:

%JAVA_HOME%\bin

Com isso, os executáveis do Java poderão ser encontrados diretamente pelo terminal, independentemente do diretório em que estivermos.

---

## 3. Verificando a instalação

Depois de configurar as variáveis de ambiente, abra um novo terminal e execute:

java -version

Se tudo estiver funcionando corretamente, o terminal deverá mostrar a versão instalada.

No meu caso:

java version "21.0.12.1" 2026-08-18 LTS

Isso confirma que o Java está instalado e disponível no Path.

Também podemos verificar o compilador do Java:

javac -version

---

# Linux

No Linux temos diversas formas de instalar o Java. Neste README vou apresentar duas delas:

1. Utilizar o gerenciador de pacotes da distribuição;
2. Utilizar o SDKMAN!, que facilita bastante o gerenciamento de diferentes versões do Java.

A primeira opção é interessante quando queremos que o próprio sistema operacional gerencie a instalação.

A segunda é especialmente útil durante o desenvolvimento, principalmente quando diferentes projetos precisam de versões diferentes do Java.

---

# Opção 1 — Gerenciador de pacotes

A primeira opção é utilizar o gerenciador de pacotes da própria distribuição.

Como cada distribuição possui seus próprios repositórios e ferramentas, os comandos podem variar.

## Arch Linux

No meu caso, utilizo Arch Linux, então podemos instalar o JDK diretamente utilizando o pacman:

sudo pacman -S jdk21-openjdk

Depois da instalação, podemos verificar:

java -version

Também podemos verificar a versão do compilador:

javac -version

Caso existam várias versões do Java instaladas no sistema, o Arch Linux fornece o archlinux-java para visualizar as versões disponíveis:

archlinux-java status

E podemos selecionar qual delas será utilizada como padrão:

sudo archlinux-java set java-21-openjdk

Depois disso, podemos confirmar novamente:

java -version

---

## Debian / Ubuntu

Em distribuições baseadas em Debian, também podemos utilizar o gerenciador de pacotes apt.

Neste exemplo, vamos utilizar o Amazon Corretto, uma distribuição do OpenJDK mantida pela Amazon.

Primeiro, precisamos importar a chave do repositório:

wget -O - https://apt.corretto.aws/corretto.key | sudo gpg --dearmor -o /usr/share/keyrings/corretto-keyring.gpg

Depois adicionamos o repositório:

echo "deb [signed-by=/usr/share/keyrings/corretto-keyring.gpg] https://apt.corretto.aws stable main" | sudo tee /etc/apt/sources.list.d/corretto.list

Agora podemos atualizar os repositórios e instalar o JDK:

sudo apt-get update
sudo apt-get install -y java-21-amazon-corretto-jdk

Por fim, verificamos a instalação:

java -version

E também podemos verificar o compilador:

javac -version

> Observação: os comandos acima são específicos para distribuições baseadas em Debian, como Ubuntu. Em outras distribuições, o processo de instalação pelo gerenciador de pacotes pode ser diferente.

---

# Opção 2 — SDKMAN!

A segunda opção é utilizar o SDKMAN!.

Essa é a forma recomendada neste ambiente para quem precisa trabalhar com diferentes versões do Java e quer conseguir trocar entre elas com facilidade.

Em vez de instalar e configurar manualmente cada versão, o SDKMAN! permite instalar, remover, listar e alternar entre diferentes versões do Java através do próprio terminal.

O SDKMAN! funciona diretamente em Linux e macOS.

No Windows, ele pode ser utilizado dentro do WSL ou do Git Bash.

---

## 1. Instalando o SDKMAN!

Para instalar o SDKMAN!, executamos:

curl -s "https://get.sdkman.io" | bash

Depois da instalação, precisamos carregar o SDKMAN! no terminal atual:

source "$HOME/.sdkman/bin/sdkman-init.sh"

Também podemos simplesmente fechar o terminal e abrir outro.

Para verificar se o SDKMAN! foi instalado corretamente:

sdk version

---

## 2. Listando as versões disponíveis

Com o SDKMAN! instalado, podemos utilizar:

sdk list java

Esse comando mostra as diferentes versões e distribuições do Java disponíveis para instalação.

Entre elas podemos encontrar, por exemplo:

- Amazon Corretto
- Eclipse Temurin
- Microsoft
- Oracle
- OpenJDK
- e outras distribuições

Isso é particularmente útil porque não ficamos limitados a uma única distribuição do JDK.

---

## 3. Instalando uma versão do Java

Depois de encontrar a versão desejada, podemos instalá-la utilizando:

sdk install java 21.0.12.1-amzn

Nesse caso, estamos instalando o Amazon Corretto 21.

Após a instalação, podemos confirmar:

java -version

E também:

javac -version

---

## 4. Trocando entre versões do Java

Uma das principais vantagens do SDKMAN! aparece quando precisamos trabalhar com mais de uma versão do Java.

Para visualizar as versões disponíveis e instaladas:

sdk list java

Podemos utilizar uma versão específica apenas no terminal atual com:

sdk use java <versao>

Por exemplo:

sdk use java 21.0.12.1-amzn

Se quisermos definir uma versão como padrão para os próximos terminais:

sdk default java <versao>

Isso torna muito mais simples trabalhar em projetos que possuem requisitos diferentes de versão.

---

# Verificando a instalação

Independentemente do método utilizado, podemos verificar se o Java está funcionando com:

java -version

Também podemos verificar o compilador:

javac -version

Um resultado semelhante a este indica que o JDK está disponível corretamente:

java 21.0.x
javac 21.0.x

É importante lembrar que estamos instalando o JDK (Java Development Kit), e não apenas o ambiente necessário para executar aplicações Java.

O java é utilizado para executar programas Java, enquanto o javac é o compilador responsável por transformar código-fonte Java em bytecode.

---

# Comparando as opções

Cada método possui uma finalidade diferente.

Método                     | Plataforma       | Principal vantagem
---------------------------|------------------|-----------------------------
Instalador Oracle          | Windows          | Instalação simples e direta
Gerenciador de pacotes     | Linux            | Integração com o sistema operacional
SDKMAN!                    | Linux / macOS    | Facilidade para instalar e trocar versões

Para uma máquina que precisa apenas de uma versão fixa do Java, utilizar o instalador da plataforma ou o gerenciador de pacotes costuma ser suficiente.

Para um ambiente de desenvolvimento onde podemos precisar trabalhar com diferentes projetos e versões do Java, o SDKMAN! se torna especialmente interessante, pois permite trocar de versão rapidamente sem precisar fazer todo o processo de instalação e configuração novamente.
