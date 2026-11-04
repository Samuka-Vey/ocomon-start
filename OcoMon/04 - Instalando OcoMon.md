# 🐳 Executando o OcoMon com Docker

🏷️ **Tags:** #docker #ocomon #tutorial #devops #containers

## 🚀 1. Executando o contêiner

Depois de baixar a imagem, execute o seguinte comando no terminal:

Bash

```
docker run -d -p 8080:80 flaviorib/ocomon:6.8.1
```

## 🔎 2. Entendendo o comando

O comando `docker run` permite criar e iniciar um contêiner a partir de uma imagem. Vamos dividir esse comando em partes para entender o que cada pedaço faz:

|**⚙️ Parâmetro**|**📖 Explicação**|
|---|---|
|`docker`|Executa o aplicativo Docker pelo terminal.|
|`run`|Cria e inicia um novo contêiner.|
|`-d`|Executa o contêiner em segundo plano (_detached_), permitindo que você continue utilizando o terminal livremente.|
|`-p 8080:80`|Faz o redirecionamento (mapeamento) de portas entre o seu computador e o contêiner.|
|`flaviorib/ocomon:6.8.1`|Identifica exatamente qual imagem será utilizada.|

## 🌐 3. Entendendo o redirecionamento de portas

Uma das partes mais importantes do comando é o `-p 8080:80`. Esse parâmetro permite que o seu computador consiga acessar a aplicação que está funcionando isolada _dentro_ do contêiner.

A estrutura padrão é: `-p PORTA_DO_COMPUTADOR:PORTA_DO_CONTAINER`

No nosso exemplo (`-p 8080:80`):

- 💻 **8080:** porta livre no seu computador (Windows, Linux ou Mac).
    
- 📦 **80:** porta padrão utilizada pelo servidor web do OcoMon dentro do contêiner.
    

> [!note] 🗺️ Como funciona o caminho dos dados?
> 
> Imagine que o OcoMon está funcionando dentro do Docker na porta 80. Para acessá-lo pelo navegador, disponibilizamos essa porta através da 8080 do nosso computador real.
> 
> Plaintext
> 
> ```
> 💻 COMPUTADOR
>       |
>       | Porta 8080
>       v
> 🐳 DOCKER
>       |
>       | Redirecionamento
>       v
> 📦 CONTAINER OCOMON
>       |
>       | Porta 80
>       v
> 🌐 SERVIDOR WEB
> ```
> 
> Por isso, ao final, podemos acessar o sistema pelo endereço: `http://localhost:8080`

> [!tip] 💡 E se eu quiser utilizar outra porta?
> 
> Você pode alterar facilmente a porta do computador caso a `8080` já esteja em uso.
> 
> Exemplo:
> 
> Bash
> 
> ```
> docker run -d -p 9090:80 flaviorib/ocomon:6.8.1
> ```
> 
> Nesse caso, o acesso será: `http://localhost:9090`. A porta interna do contêiner continua sendo `80`, apenas a porta externa da sua máquina mudou.

## 📦 4. Entendendo o nome da imagem

No final do comando temos o nome completo da imagem: `flaviorib/ocomon:6.8.1`. Essa identificação possui três partes fundamentais:

|**🏷️ Parte**|**📌 Significado**|
|---|---|
|`flaviorib`|Nome do usuário ou organização que publicou a imagem no Docker Hub.|
|`ocomon`|Nome da imagem propriamente dita (o software).|
|`6.8.1`|Versão (_tag_) específica da imagem.|

Com essa estrutura, o Docker sabe com exatidão qual imagem (e versão) deve utilizar para criar o contêiner, evitando instalar versões desatualizadas ou instáveis por engano.

## 🧠 5. Resumo da Ópera

Ao executar o comando `docker run -d -p 8080:80 flaviorib/ocomon:6.8.1`, o Docker realiza as seguintes operações nos bastidores:

1. 🔎 **Procura** a imagem do OcoMon salva localmente no seu computador.
    
2. 📥 **Baixa** (faz o _pull_) da imagem do repositório oficial caso não a encontre na sua máquina.
    
3. 📦 **Cria** um novo contêiner zerado.
    
4. 🚀 **Inicia** o contêiner em segundo plano.
    
5. 🌐 **Disponibiliza** o acesso externo pela porta 8080.
    

> [!success] 🎉 Resultado final
> 
> O sistema de chamados OcoMon estará totalmente disponível e pronto para uso! Basta abrir o seu navegador e acessar **[http://localhost:8080](http://localhost:8080/)**.****