# Ambiente Local de Desenvolvimento Next.js utilizando Dev Container

O projeto `nextjs-dev-container` visa criar um ambiente de desenvolvimento consistente e replicável para projetos Next.js, utilizando o Visual Studio Code, Dev Container e Docker. A motivação por trás desse projeto surgiu durante minha jornada no curso.dev, que utiliza GitHub Codespaces como ambiente de desenvolvimento. Entretanto, desejei explorar a criação de um ambiente semelhante em meu próprio computador, visando aprender e compartilhar uma estrutura que simplificasse o início de novos projetos com a mesma configuração.

## O que você precisa para começar

Certifique-se de ter as seguintes ferramentas instaladas em seu sistema:

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker](https://www.docker.com/get-started)
- [Extensão Dev Containers para o Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Clonando e Configurando o Projeto

1. Clone este repositório para sua máquina local:

```bash
git clone https://github.com/adspacheco/nextjs-dev-container.git
```

2. Abra o projeto no Visual Studio Code com a extensão Dev Containers habilitada. Você será solicitado a reabrir o projeto no Dev Container.

```bash
cd nextjs-dev-container
code .
```

3. Depois de reabrir o projeto, você estará pronto para começar.

## Entendendo o Dev Container e Docker in Docker

### Dev Container

O Dev Container é uma extensão do Visual Studio Code que permite criar ambientes de desenvolvimento isolados e consistentes.

### Docker outside of Docker

Dentro do ambiente de desenvolvimento, usei uma técnica chamada "Docker outside of Docker". Isso significa que o VSCode reutiliza o socket do Docker do host local, adicionando o Docker CLI a um contêiner. Essa funcionalidade permite executar comandos Docker diretamente dentro do Dev Container, aproveitando o Docker instalado em sua máquina host. Isso elimina a necessidade de instalar o Docker diretamente no Dev Container, mantendo as operações de contêineres no contexto do Docker da máquina local.

### Comunicação com o Banco de Dados

Devido ao uso do Docker outside of Docker, a comunicação com os serviços Docker do host local, como o banco de dados PostgreSQL, é feita de forma especial. Em vez de usar `localhost` para se comunicar com o banco de dados, usa `host.docker.internal`.

Isso ocorre porque o contêiner Dev Container é uma máquina virtual isolada, e o `localhost` dentro do contêiner se refere ao próprio contêiner, não ao host local. Usando `host.docker.internal`, é possível acessar os serviços do host local a partir do contêiner.

## Iniciando o Ambiente de Desenvolvimento

Agora que você configurou o projeto e entende como o Dev Container e o Docker outside of Docker funcionam, você pode iniciar seu ambiente de desenvolvimento. Isso envolve iniciar o contêiner Docker que executa o banco de dados PostgreSQL e iniciar o servidor Next.js. Você pode fazer isso executando o seguinte comando no terminal do Visual Studio Code:

```bash
npm run dev
```

Isso executará os seguintes passos automaticamente:

- Inicializará o contêiner Docker com o PostgreSQL.
- Iniciará o servidor Next.js.

A partir deste ponto, você poderá acessar sua aplicação Next.js em [http://localhost:3000](http://localhost:3000) e interagir com seu banco de dados PostgreSQL usando a configuração definida no arquivo `.env.development`.

## Comandos Úteis

- Para parar o ambiente de desenvolvimento, você pode usar o seguinte comando:

```bash
npm run services:stop
```

- Para encerrar e remover os contêineres Docker associados, use:

```bash
npm run services:down
```

## Personalizações e Extensões Recomendadas

No projeto, já incluí algumas configurações e extensões recomendadas para melhorar a experiência de desenvolvimento:

- Tema do VS Code: Dracula.
- Formatação automática com Prettier.
- Configurações específicas para o editor estão disponíveis no arquivo `settings.json`.

## Todo

[ ] Aprimorar a inicialização do container
[ ] Trocar a imagem da Microsoft por uma imagem oficial do Node.js
[ ] Comentar o código para relembrar as configurações que fiz
[ ] Dar os créditos e referência de onde encontrei as soluções
[ ] Melhorar o README

---

# Créditos

Este projeto foi desenvolvido com base na inspiração e aprendizado obtidos durante minha jornada no curso.dev. Agradeço ao Felipe Deschamps por compartilhar seu conhecimento e por fornecer as bases que tornaram possível a criação deste ambiente de desenvolvimento.

Este projeto é uma pequena forma de retribuir e compartilhar o conhecimento com a comunidade de desenvolvedores.
