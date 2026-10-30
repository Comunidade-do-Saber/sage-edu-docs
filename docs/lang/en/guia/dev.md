## 📘 Development Environment

In this section we present all the steps necessary to configure the **SAGE Edu** development environment, including system preparation, configuration of dependencies and installation of the Tryton modules used by the project.


### 🖥️ 1. Environment Preparation

Before getting started, we recommend creating an isolated development environment, especially if you need to work with multiple versions of Python.
For this we will use [virtualenv](https://virtualenv.pypa.io/en/latest/).

* 🔧 Virtualenv Installation

On Debian-based Linux distributions, install Python 3 and virtualenv with:

```bash
sudo apt install python3 virtualenv
```

* 🧪 Creation of the Virtual Environment

Create and activate a unique virtual environment for SAGE Edu:

```bash
virtualenv sage_edu_env

source sage_edu_env/bin/activate
```


### 🏗️ 2. Installation and Configuration

SAGE Edu uses Tryton as its base framework and PostgreSQl as its database manager.
Install the necessary packages within the virtual environment:

#### 📦 PostgreSQL Installation

```bash
sudo apt install postgresql postgresql-contrib
```

👤 **Create User**

```bash
sudo su postgres -c "createuser -s sage_edu"

sudo su postgres -c "psql -c \"ALTER ROLE sage_edu WITH PASSWORD 'sage_edu'\""
```

⚙️ **PostgreSQL Configuration**

Some files need to be adjusted to allow proper access.

* Edit pg_hba.conf

Find and change the line below:
```bash
DE: 
    local         all            all                        peer

PARA:
    local         all            all                        md5
```

* Edit postgresql.conf

Enable the network listening parameter:
```bash
listen_addresses = '*'
```
Remove the ; at the beginning if it exists.

* Restart the servic

```bash
sudo systemctl restart postgresql
```

🗄️ **Create the Data Base**

```bash
createdb -U sage_edu sage_edu_db
```


#### 📦 Trytond Installation

```bash
pip install psycopg2-binary

pip install pycountry

pip install trytond~=8.0.0
```


📝 **Create the file trytond.conf**

Create the Tryton server configuration file:

```bash
touch trytond.conf
```

Add content:

```bash
[database]
uri = postgresql://sage_edu:sage_edu@localhost:5432/sage_edu_db
```

* 🔧 Initialize the Database

```bash
trytond-admin -c trytond.conf -d sage_edu_db --all
```

🚀 **Start Tryton Server**

```bash
trytond -c trytond.conf
```

#### 📦 SAGE Edu Modules Installation

After the Tryton environment is configured, install the official SAGE Edu modules directly from GitHub:

```bash
git clone https://github.com/comunidade-do-saber/akademy-party
git clone https://github.com/comunidade-do-saber/akademy-company
git clone https://github.com/comunidade-do-saber/akademy-classe
git clone https://github.com/comunidade-do-saber/akademy-classe-evaluation
git clone https://github.com/comunidade-do-saber/akademy-matriculation
git clone https://github.com/comunidade-do-saber/akademy-matriculation_confirmation
```

💡 Note: After installing new modules, it is recommended to restart the Tryton server and run trytond-admin again to synchronize the tables.