# ansible-harbor

Usage your certificate or generate self singend from official instruction https://goharbor.io/docs/2.0.0/install-config/configure-https/

After that, just copy your certificate in ./roles/harbor/files directory.

Edit ./roles/harbor/defaults/main.yaml if nessesary and run

```bash
ansible-playbook ansible/playbook/harbor.yaml
```
