### 📋 Instalação

Para fazer a instalação do SAGE Edu, você pode faze-lo pelo pip de instalação ou usar a nossa imagem docker.

##### 🐳 Quick Start with Docker (Recommended)

A maneira mais rápida de testar o SAGE Edu v2.0 é usando nossa imagem Docker oficial:

```bash
git clone https://github.com/comunidade-do-saber/sage-edu.git
cd sage-edu/docker
docker compose up -d
```

Após a execução, o servidor estará disponível em `http://localhost:8000`.

##### 🔧 Instalação via PIP (Manual)

Também é possível instalar o SAGE Edu manualmente utilizando o `pip`.
Para isso, será necessário:

* **PostgreSQL** instalado e configurado:
    * Criar um usuário e definir permissões.
    * Criar a base de dados (ex: `sage_education`).

* **Cliente Tryton** (Desktop ou Web) instalado para acessar o sistema:
    * [Tryton Desktop Client](https://www.tryton.org/)
    * [Tryton Web Client](https://www.npmjs.com/package/tryton-sao)

**1. Instalar os módulos via PIP**

```bash
pip install trytond==8.0
pip install akademy-party==8.0.0
pip install akademy-company==8.0.0
pip install akademy-classe==8.0.0
pip install akademy-classe-evaluation==8.0.0
pip install akademy-matriculation==8.0.0
pip install akademy-matriculation-confirmation==8.0.0
```

**2. Criar o arquivo de configuração do Tryton (`trytond.conf`)**

Crie um arquivo com o seguinte conteúdo, ajustando `usuario`, `senha` e `banco_de_dados` conforme a sua configuração local:

```ini
[database]
uri = postgresql://usuario:senha@localhost:5432/banco_de_dados

[web]
listen = 0.0.0.0:8000
```

**3. Inicializar o banco de dados**

Execute o comando abaixo para criar todas as tabelas e carregar os dados iniciais dos módulos:

```bash
trytond-admin -c /caminho/para/trytond.conf -d nome_do_banco --all
```

**4. Iniciar o servidor**

```bash
trytond -c /caminho/para/trytond.conf
```

Agora você pode acessar o SAGE Edu através do seu cliente Tryton (Desktop ou Web) utilizando o endereço do servidor.
