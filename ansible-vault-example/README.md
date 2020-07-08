Ansible Vault example
======================

### use ansible vault file

1. create a file to store vault password for encrypting variables

  > echo "secret_password" > .vault_password

2. create a vault file that `group_vars/all` to save db password. vault password is saved in `.vault_password` which we created.

  > ansible-vault --vault-password-file=.vault_password create group_vars/all

  `all` file's original details:

  ```yml
  ---
  db_password: test
  ```

  after encrypt:
  ```
    $ANSIBLE_VAULT;1.1;AES256
  37633561393332353064356439373636306438663131666431636637313738323036623838633730
  6637653533306230363238656134336432623563623731390a346663646662386163626262386439
  65303862363734396633386630323338393931303339613063313631633465626239396261353432
  3665666635373534340a616561346438323866353536373139323136633962343733356565353136
  61636335623561646361346563396633636534653934316236396330343963373765
  ```

3. place `db_password` in `roles/vault-role/tasks/main.yml`.

  ```yml
  # tasks file for vault-role
  - debug:
      msg: "{{db_password}}"
  ```

4. run ansible playbook

  ```sh
  ansible-playbook --vault-password-file=.vault_password  -i inventory playbook.yml
  ```

  then the ansible logs like this:
  ```
  PLAY [node] ************************************************************************************************************************************************

  TASK [Gathering Facts] *************************************************************************************************************************************
  ok: [192.168.12.10]

  TASK [vault-role : debug] **********************************************************************************************************************************
  ok: [192.168.12.10] => {
      "msg": "test"
  }

  PLAY RECAP *************************************************************************************************************************************************
  192.168.12.10              : ok=2    changed=0    unreachable=0    failed=0
  ```
