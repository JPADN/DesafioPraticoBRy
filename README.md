# Desafio Prático do Processo Seletivo BRy
## Desenvolvedor Full Stack Java

Para clonar este repositório junto com seus submódulos, execute: 
```
git clone --recurse-submodules git@github.com:JPADN/DesafioPraticoBRy.git no README
```

### Etapas 1, 2 e 3

As etapas 1, 2 e 3 estão implementadas no repositório SigningUtilities, pelo método main da classe Main. A etapa 1 prevê como saída um documento contendo o resultado do resumo criptográfico em hexadecimal, a etapa 2 prevê como saída um documento do tipo ".p7s" com a assinatura digital, enquanto que a etapa 3 prevê como saída um print no terminal de true (caso a assinatura seja válida) ou false (caso a assinatura seja inválida).

Para as etapas que geram documentos como saída, estes estarão disponíveis após a execução da aplicação no diretório `SigningUtilities/etapas_1_2_output`. A saída prevista pela Etapa 1 está nomeada como `doc_hex_digest.txt` enquanto que a da Etapa 2 está nomeada como `doc_signature.p7s`.

(Estes mesmos arquivos podem ser encontrados também no diretório `anexos/`)

O JAR desta aplicação encontra-se em `SigningUtilities/out/artifacts/SigningUtilities_jar/SigninUtilities.jar`, e para executá-lo em um ambiente Docker é disponibilizado um Dockerfile em `SigningUtilities/Dockerfile`

A fim de compilar a imagem Docker e iniciar um container a partir desta, execute os seguintes comandos no diretório raiz de SigningUtilities:

```
docker build . -t signing-utilities
docker run -v ${PWD}/etapas_1_2_output:/app/etapas_1_2_output signing-utilities
```

Note que é necessário declarar o volume (argumento `-v`) para que os documentos produzidos pela aplicação estejam disponíveis no sistema de arquivos do host. `PWD` é uma variável de ambiente do Linux, caso você esteja executando em outro sistema operacional, substitua `${PWD}` pelo caminho **absoluto** do diretório onde você deseja que os arquivos sejam salvos.

### Etapa 4

Trata-se uma API Rest utilizando o framework Spring Boot e reutilizando o código criado nas etapas anteriores. Esta etapa foi implementada no repositório SignApp.

Para que seja possível reutilizar o código das etapas anteriores, o JAR da aplicação SigningUtilities foi adicionado como dependência para a compilação do JAR de SignApp, desta forma as classes definidas em SigningUtilities ficam disponíveis para uso pelo SignApp.

O JAR desta aplicação encontra-se em `SignApp/out/artifacts/signapp_jar/signapp.jar`, e para executá-lo em um ambiente Docker é disponibilizado um Dockerfile em `SignApp/Dockerfile`.

A fim de compilar a imagem Docker e iniciar um container a partir desta, execute os seguintes comandos no diretório raiz de SignApp:

```
docker build . -t signapp
docker run -p 8080:8080 signapp
```

Note que é necessário publicar a porta 8080 do container para a porta 8080 do host. Após isto, a API encontra-se disponível em `http://localhost:8080`.

### Etapa 5

O relatório de atividades encontra-se disponível em `relatorio.pdf`.
