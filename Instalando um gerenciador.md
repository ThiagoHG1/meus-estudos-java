# Principais Gerenciadores de Build em Java

Em projetos Java, o código-fonte não é a única coisa que precisamos organizar. Também precisamos gerenciar dependências, compilar o projeto, executar testes, empacotar a aplicação e, em muitos casos, automatizar outras etapas do processo de desenvolvimento.

É para isso que entram os **gerenciadores de build**.

Atualmente, os dois principais gerenciadores de build encontrados no ecossistema Java são o **Maven** e o **Gradle**.

---

## Maven

O **Maven** é uma ferramenta tradicional e muito utilizada no mercado, principalmente em ambientes corporativos.

Ele segue o princípio de **"convenção sobre configuração"** (*Convention over Configuration*). A ideia é estabelecer uma estrutura e alguns comportamentos padrão para que o desenvolvedor precise configurar apenas aquilo que realmente foge do padrão.

A configuração do projeto normalmente fica no arquivo:

```text
pom.xml
```

Esse arquivo utiliza **XML** para definir informações como:

- dependências;
- versão do Java;
- plugins;
- etapas do build;
- configuração do projeto.

Por seguir uma estrutura bastante padronizada, o Maven pode ser mais previsível de entender quando pegamos um projeto que segue suas convenções.

---

## Gradle

O **Gradle** é uma ferramenta mais moderna e flexível.

Em vez de utilizar XML como o Maven, o Gradle utiliza arquivos de build baseados em scripts. Esses scripts podem ser escritos em **Groovy** ou **Kotlin**.

O arquivo mais comum é:

```text
build.gradle
```

Também podemos encontrar:

```text
build.gradle.kts
```

quando o projeto utiliza a sintaxe baseada em Kotlin.

Por ser baseado em scripts, o Gradle permite uma configuração mais personalizada e expressiva, sendo bastante útil quando o projeto possui necessidades que vão além do fluxo padrão.

---

# Maven x Gradle

Os dois resolvem problemas muito parecidos, mas seguem abordagens diferentes.

| Característica | Maven | Gradle |
|---|---|---|
| Configuração principal | `pom.xml` | `build.gradle` / `build.gradle.kts` |
| Formato | XML | Groovy / Kotlin |
| Filosofia | Convenção sobre configuração | Flexibilidade e configuração programática |
| Estilo | Mais padronizado | Mais personalizável |
| Uso no mercado | Muito comum, especialmente em empresas | Muito comum e bastante utilizado em projetos modernos |

Não existe uma regra de que um é simplesmente "melhor" que o outro. A escolha depende do projeto, da equipe e do ecossistema utilizado.

---

# Instalando o Maven no Windows

Existem diferentes formas de instalar o Maven.

A forma apresentada aqui é a **instalação manual**, que é mais engessada. O Junior reforça no vídeo que prefere utilizar o **SDKMAN!** para gerenciar esse tipo de ferramenta, mas demonstra a instalação manual porque ela é útil em determinadas situações.

Um exemplo seria um servidor no qual queremos manter uma **versão fixa** do Maven e não precisamos trocar de versão com frequência.

## 1. Baixando o Maven

Acesse o site oficial:

https://maven.apache.org/download.cgi

Na página de download, procure pelo:

**Binary zip archive**

Baixe o arquivo `.zip` e extraia o conteúdo em uma pasta dentro do seu usuário.

Por exemplo:

```text
C:\Users\seu-usuário\maven
```

Evite extrair diretamente na raiz:

```text
C:\maven
```

No Windows, isso pode causar problemas relacionados a permissões dependendo da configuração do sistema.

---

## 2. Configurando as variáveis de ambiente

Depois de extrair o Maven, precisamos configurar as variáveis de ambiente.

Primeiro, crie uma variável chamada:

```text
MAVEN_HOME
```

Ela deve apontar para a pasta onde o Maven foi extraído.

Por exemplo:

```text
MAVEN_HOME=C:\Users\seu-usuário\maven
```

Depois, adicione o diretório `bin` do Maven à variável `Path`:

```text
%MAVEN_HOME%\bin
```

Isso permitirá executar o comando `mvn` diretamente pelo terminal.

---

## 3. Verificando a instalação

Depois de configurar as variáveis de ambiente, abra um **novo terminal**.

Isso é importante porque terminais que já estavam abertos podem não possuir as novas variáveis de ambiente.

Execute:

```bash
mvn -version
```

Se tudo estiver configurado corretamente, o Maven deverá exibir informações sobre a versão instalada, o Java utilizado e o sistema operacional.

---

# Instalando o Gradle no Windows

Assim como no Maven, aqui também estamos utilizando a **instalação manual**.

A própria documentação oficial do Gradle recomenda alternativas como o SDKMAN! para facilitar o gerenciamento da ferramenta, mas a instalação manual continua sendo importante de conhecer.

Ela pode ser útil, por exemplo, em um ambiente no qual queremos instalar uma versão específica e mantê-la fixa.

## 1. Baixando o Gradle

Acesse a página oficial de releases:

https://gradle.org/releases/

Escolha a versão desejada e procure pelo pacote:

**Binary-only**

Baixe o arquivo `.zip` e extraia dentro de uma pasta do seu usuário, seguindo a mesma lógica utilizada no Maven.

Por exemplo:

```text
C:\Users\seu-usuário\gradle-8.13
```

ou em uma organização própria:

```text
C:\Users\seu-usuário\gradle\gradle-8.13
```

O importante é saber exatamente qual pasta contém a instalação do Gradle.

---

## 2. Configurando as variáveis de ambiente

Agora precisamos configurar a variável:

```text
GRADLE_HOME
```

Ela deve apontar para a pasta onde o Gradle foi extraído.

Por exemplo:

```text
GRADLE_HOME=C:\Users\seu-usuário\gradle-8.13
```

Depois, adicione o diretório `bin` do Gradle à variável `Path`:

```text
%GRADLE_HOME%\bin
```

Assim como no Maven, isso permite executar o Gradle diretamente pelo terminal.

---

## 3. Verificando a instalação

Abra um novo terminal e execute:

```bash
gradle -v
```

Se tudo estiver configurado corretamente, o Gradle exibirá informações sobre a versão instalada, a JVM utilizada e o ambiente em que está sendo executado.

---

# Por que conhecer a instalação manual?

Mesmo que ferramentas como o **SDKMAN!** sejam mais práticas para desenvolvimento local, conhecer a instalação manual continua sendo útil.

Em determinadas situações, podemos trabalhar em uma máquina em que:

- não queremos adicionar outra ferramenta de gerenciamento;
- precisamos manter uma versão específica;
- estamos configurando um servidor;
- precisamos entender como as variáveis de ambiente e os executáveis estão organizados.

Por isso, vale a pena conhecer os dois métodos: a instalação manual ajuda a entender como o ambiente funciona, enquanto uma ferramenta como o SDKMAN! facilita o gerenciamento no dia a dia.

---
