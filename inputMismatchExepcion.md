# Aprendendo com um erro simples de localização no Java

## Contexto

Durante meus primeiros estudos com Java, estava fazendo um programa bem simples: receber o tamanho de um lado de um quadrado e calcular sua área.

O código inicialmente estava assim:

```java
import java.util.Scanner;

public class App {
    public static void main(String[] args) throws Exception {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Por favor, insira o tamanho de um lado do quadrado: ");
        double sideSize = scanner.nextDouble();

        System.out.printf("A area do quadrado é %s.\n", Math.pow(sideSize, 2.0d));
    }
}
```

A lógica era extremamente simples, então achei que seria algo tranquilo de testar:

```text
17.0
```

Só que o programa retornou uma `InputMismatchException`.

E foi aí que começou uma pequena investigação que acabou me ensinando algo que eu ainda não tinha percebido sobre o Java.

---

## O primeiro palpite

Naquele momento, meu raciocínio foi mais ou menos:

> "Input? Deve ser porque meu `sideSize` está como `float` e o `Math.pow()` precisa de `double`."

Então alterei a variável para:

```java
double sideSize = scanner.nextDouble();
```

Tentei novamente:

```text
17.0
```

E o erro continuou.

Então pensei:

> "Será que eu tenho que colocar o `d` no terminal?"

Tentei:

```text
17.0d
```

E, obviamente, também não funcionou.

---

## O que estava acontecendo?

O problema não tinha relação com `float`, `double` ou com o `Math.pow()`.

O problema estava no **locale utilizado pelo `Scanner`**.

O `Scanner` utiliza uma configuração de localização para interpretar determinados valores recebidos como texto. Essa configuração define, entre outras coisas, qual caractere deve ser utilizado como separador decimal.

Em um locale como o dos Estados Unidos:

```text
17.0
```

é interpretado como um número decimal.

Já em um locale que utiliza a convenção brasileira:

```text
17,0
```

é a representação esperada.

Como meu sistema estava configurado em português do Brasil, o `Scanner` estava esperando:

```text
17,0
```

e não:

```text
17.0
```

Por isso:

```text
17.0
```

gerava:

```text
InputMismatchException
```

Enquanto:

```text
17,0
```

funcionava.

---

## Outra coisa que aprendi

Também percebi uma diferença importante entre **código Java** e **entrada do usuário**.

Quando escrevemos um número decimal diretamente no código Java, utilizamos ponto:

```java
double sideSize = 17.0;
```

ou:

```java
double sideSize = 17.0d;
```

O `d` nesse caso é um sufixo que pode ser utilizado no próprio código-fonte Java para indicar um literal `double`.

Mas quando fazemos:

```java
scanner.nextDouble();
```

o programa está recebendo **texto digitado pelo usuário** e tentando convertê-lo para um `double`.

Nesse caso, escrever:

```text
17.0d
```

não faz sentido para o `Scanner`, porque `d` não faz parte da representação numérica que ele está esperando.

---

# Controlando o Locale

Depois de entender a causa do problema, descobri a classe:

```java
java.util.Locale
```

Ela permite especificar qual configuração regional queremos utilizar.

Para utilizar o padrão dos Estados Unidos, podemos fazer:

```java
Scanner scanner = new Scanner(System.in).useLocale(Locale.US);
```

Assim, o `Scanner` passa a interpretar:

```text
17.0
```

como um `double` normalmente.

O programa ficou assim:

```java
import java.util.Scanner;
import java.util.Locale;

public class App {
    public static void main(String[] args) throws Exception {
        Scanner scanner = new Scanner(System.in).useLocale(Locale.US);

        System.out.print("Por favor, insira o tamanho de um lado do quadrado: ");
        double sideSize = scanner.nextDouble();

        System.out.printf(Locale.US, "A area do quadrado é %s.\n", Math.pow(sideSize, 2.0d));
    }
}
```

Agora posso executar o programa e informar:

```text
17.0
```

sem receber a exceção.

---

# E qual seria a forma mais adequada?

No meu caso, como o programa está em português e estou utilizando um sistema configurado para o Brasil, provavelmente faria mais sentido seguir o padrão local e simplesmente informar:

```text
17,0
```

em vez de forçar `Locale.US`.

Ou seja, **não existe necessariamente um problema com o locale brasileiro**. O problema foi que eu estava digitando a entrada utilizando uma convenção diferente daquela que o `Scanner` estava configurado para interpretar.

Mesmo assim, essa pequena situação foi útil porque me fez descobrir algo que eu ainda não conhecia sobre o Java.

---

# O que eu aprendi

Apesar de o programa ser extremamente simples, esse erro acabou me ensinando algumas coisas importantes:

- `Scanner.nextDouble()` leva o `Locale` em consideração ao interpretar a entrada.
- O separador decimal pode variar de acordo com a localização configurada.
- O sufixo `d` faz parte da sintaxe do código Java e não deve ser digitado na entrada do `Scanner`.
- `java.util.Locale` permite controlar a convenção regional utilizada pelas APIs que dependem de localização.
- Um erro em algo aparentemente trivial pode revelar detalhes importantes sobre como uma linguagem e suas bibliotecas funcionam.

## Conclusão

Esse foi um daqueles erros que parecem completamente idiotas depois que você descobre a causa.

Eu estava tentando resolver o problema olhando para o tipo da variável, para o `Math.pow()` e até para a representação do `double`, quando na verdade o problema estava na forma como o **texto digitado estava sendo interpretado pelo `Scanner`**.

Foi uma coisa pequena, mas gostei de ter encontrado o motivo em vez de simplesmente trocar o código até funcionar.

No fim das contas, mais uma coisa para guardar na cabeça:

> Nem todo erro de conversão é sobre o tipo. Às vezes é sobre a forma como o valor está sendo interpretado.
