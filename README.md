# CKA training and good to remembers :)

when you init a cluster, with that output is a pre-created `kubeadm- join`, with that command is a token and a sha256 key. For many reasons that command won't last. The token only lasts 2 hours and typically you can forget / lose the sha key. Below are the commands to run so that you can coalesce all the pieces without the pre-generated `kubeadm join` command.

`sudo kubeadm token create`

`sudo kubeadm token list`

`openssl x509 -pubkey -in /etc/kiubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dget -sha256 -hex | sed 's/^.* //'`

`kubeadm join --token <the_token> <ip||dns>:<port> --discovery-token-ca-cert-hash sha256:<cert_from_openssl_cmd>`
