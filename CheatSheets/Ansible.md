## Ansible Basic Commands Cheatsheet

| **command**                                                   | **result**                                                              |
| ------------------------------------------------------------- | ----------------------------------------------------------------------- |
| ansible-playbook -i inventory playbook.yaml                   | runs ansible playbook on specified inventory                            |
| ansible-playbook -i inventory playbook.yaml --check           | runs ansible playbook on specified inventory as a "dry run"             |
| ansible-playbook -i inventory playbook.yaml --ask-pass        | runs ansible playbook on specified inventory and asks for user password |
| ansible-playbook -i inventory playbook.yaml --ask-become-pass | runs ansible playbook on specified inventory and asks for sudo password |
|                                                               |                                                                         |

## Ansible-Vault Cheatsheet

| **command**                                         | **result**                                                                                                            |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| ansible-vault encrypt *filename*                    | encrypts file                                                                                                         |
| ansible-vault decrypt *filename*                    | decrypts file                                                                                                         |
| ansible-vault view *filename*                       | view the content of the encrypted file in clear text                                                                  |
| ansible-vault edit *filename*                       | edit the content of the decrypted file                                                                                |
| ansible-vault rekey *filename*                      | change the password of the encrypted file                                                                             |
| ansible-playbook *file.yaml* --ask-vault-pass       | run a playbook and ask for the vault password of the encrypted file where the veriable (i.e. a password) is stored.   |
| ansible-playbook *file.yaml* --vault--password-file | run a playbook and use a password file to encrypt the file where the variable is stored (make sure permission is 600) |
