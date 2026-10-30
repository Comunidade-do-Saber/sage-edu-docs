### 📋 SAGE Edu Installation

To install SAGE Edu, you can do it via `pip` or use our official Docker image.

---

##### 🐳 Quick Start with Docker (Recommended)

The fastest way to test SAGE Edu v2.0 is using our official Docker image:

```bash
git clone https://github.com/comunidade-do-saber/sage-edu.git
cd sage-edu/docker
docker compose up -d
```

After execution, the server will be available at `http://localhost:8000`.

---

##### 🔧 Manual Installation via PIP

You can also install SAGE Edu manually using `pip`.
To do this, you will need:

* **PostgreSQL** installed and configured:
    * Create a user and set permissions.
    * Create the database (e.g., `sage_education`).

* **Tryton Client** (Desktop or Web) installed to access the system:
    * [Tryton Desktop Client](https://www.tryton.org/)
    * [Tryton Web Client](https://www.npmjs.com/package/tryton-sao)

**1. Install the modules via PIP**

```bash
pip install trytond==8.0.0
pip install akademy-party==8.0.0
pip install akademy-company==8.0.0
pip install akademy-classe==8.0.0
pip install akademy-classe-evaluation==8.0.0
pip install akademy-matriculation==8.0.0
pip install akademy-matriculation-confirmation==8.0.0
```

**2. Create the Tryton configuration file (`trytond.conf`)**

Create a file with the following content, adjusting `user`, `password`, and `database_name` according to your local setup:

```ini
[database]
uri = postgresql://user:password@localhost:5432/database_name

[web]
listen = 0.0.0.0:8000
```

**3. Initialize the database**

Run the command below to create all tables and load the initial data for the modules:

```bash
trytond-admin -c /path/to/trytond.conf -d database_name --all
```

**4. Start the server**

```bash
trytond -c /path/to/trytond.conf
```

Now you can access SAGE Edu through your Tryton client (Desktop or Web) using the server address.