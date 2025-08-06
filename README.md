# scored-task2
# Automated LAMP Stack Deployment using Ansible

## 📌 Overview
This project provides a fully automated and modular Ansible setup to deploy a *LAMP stack* (Linux, Apache, MySQL, PHP) on multiple servers.  
It follows Ansible best practices using roles, handlers, error handling, and environment-based inventory management.

---

## 📁 Project Structure

bash
lamp-ansible/
├── inventories/
│   ├── dev/
│   │   └── hosts
│   └── prod/
│       └── hosts
├── playbook.yml
├── roles/
│   ├── apache/
│   ├── mysql/
│   ├── php/
│   └── firewall/
└── README.md


---

## 🚀 How to Use

### 1. Clone the Repository
bash
git clone https://github.com/aliahmed252/scored-task2.git
cd lamp-ansible


### 2. Setup Inventory

Modify the inventory files under inventories/dev/hosts or inventories/prod/hosts:

ini
[webservers]
192.168.1.101 ansible_user=root
192.168.1.102 ansible_user=root


### 3. Run the Playbook

To run against the dev environment:
bash
ansible-playbook -i inventories/dev/hosts playbook.yml


To run against the prod environment:
bash
ansible-playbook -i inventories/prod/hosts playbook.yml


---

## 🧱 Playbook Structure & Logic

- *Roles*:
  - apache: Installs and configures Apache, deploys a sample index.php.
  - mysql: Installs MySQL, secures installation, and sets root password.
  - php: Installs PHP and verifies it with Apache.
  - firewall: (optional) Adds UFW rules for HTTP/HTTPS ports.

- *Blocks & Error Handling*:
  Each major task uses block, with rescue and always sections to:
  - Handle installation errors.
  - Log issues and ensure cleanup or retries when needed.

- *Handlers*:
  Used to restart Apache automatically after configuration changes.

- *Includes*:
  Reusable tasks are broken into smaller YAML files and imported or included where necessary.

---

## 🛡 Firewall Configuration

The firewall role uses ufw to:
- Allow ports *80 (HTTP)* and *443 (HTTPS)*
- Enable the firewall if not active

---

## 📝 Notes

- Make sure to **update your ansible.cfg** if you use a custom inventory path.
- Passwords can be managed using *Ansible Vault* for better security.
- Make sure *Postfix* is installed if you integrate alerting.

---

## ✅ Requirements

- Ansible 2.9+
- Ubuntu/Debian-based servers (adjust roles for other OS types if needed)
- SSH access to target servers

---

## 📬 Contact

For any suggestions or issues, feel free to open an issue or pull request.
