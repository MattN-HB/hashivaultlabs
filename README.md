# hashivaultlabs
Recently, took great hands on course with [Hashi Vault](https://www.hashicorp.com/products/vault). This is to share the knowledge and lessons learned during it. All the commands from vault labs and [presentations directory ](https://github.com/MattN-HB/hashivaultlabs/tree/main/guides-presentations)as outlined in the [agenda](https://github.com/MattN-HB/hashivaultlabs/blob/main/guides-presentations/Vault%20Enterprise%20Academy%20Agenda%20-%203%20Day.pdf)

*Disclaimer most of the formatting is quick dumps with no clean-up so apologize ahead a time for lack of formatting. All tokens / keys stored in the commands are lab only and to show example.

## When use vault instead of cloud secrets manager (e.g.aws secrets manager): 
* multicloud
* dynamic key generation
* on prem implentation
* airgapped environments or where classified cloud is not

## How to store keys
* HSM
* Transit vault (best used in airgapped)
* KMS (aws or gcp) / [keybase](keybase.io)

## Important Commands
* first operation required after installing and launching a new vault cluster? ```vault init```
* unseel ```vault operator unseal $(cat /home/ubuntu/<directory>/<yourkeyfile>)
* validate health and grab license ```consul members vault status consul license get vault read sys/license```
* root token discovery ```cat /root/config-files/vault/initialization.txt | grep Root```
* what is my token ```echo $VAULT_TOKEN```
* address of my vault server ```echo $VAULT_ADDR```
* enable instance kv secrets engine ```vault secrets enable -path=secret kv```
* list secret engines ```vault secrets list```
* when want login in vault server to have right privs via token ```vault login -method=token <admintoken>```
* when want login in vault server to have right privs via userpass ```vault login -method=userpass username=<username> password=<password>```
* write a secret as that user ```vault kv put kv/users/cary/bio lastname=Grant age=99 gender=male```
* enable userpass in a namespace ```vault auth enable userpass```
* get a secret ```vault kv get kv/shared/passwords```
* get a version ```vault kv get -version=2 kv/customers/Sam```
* deletes only latest version ```vault kv delete kv/customers/Sam```
* undelete ```vault kv undelete -versions=6 kv/customers/Sam```
* destroy a secret ```vault kv destroy -versions=6 kv/customers/Sam```
* destroy all versions and metadata ```vault kv metadata delete kv/customers/Sam```
* create and set delete on ttl ```vault kv metadata put -delete-version-after=60s kv/customers/Sam/password```
* unset namespace ```unset VAULT_NAMESPACE```
* create namespace ```vault namespace create <nameofnamespace>```
* export vault_namespace ```export VAULT_NAMESPACE=<nameofnamespace>```
* unset vault token to attempt login other user ```unset VAULT_TOKEN```
* api endpoint vault health ```/sys/health/```
* api endpoint for unseal vaut ```/sys/unseal/```
* enable aws auth ```vault auth enable aws```
* Setup Vault with AWS ```$ vault write auth/aws/config/client secret_key=vCtSM8ZUEQ3.... access_k```
* AWS IAM authentication ```$ vault write auth/aws/role/dev-role-iam auth_type=iam \
bound_iam_principal_arn=arn:aws:iam::123456789012:role/MyRolepolicies=prod,dev max_ttl=500h```
* EC2 Authentication ```$ vault write auth/aws/role/dev-role auth_type=ec2 bound_ami_id=ami-fce3 policies=prod,dev max_ttl=500h```
* enable approle for auth ```vault auth enable -description="AppRole auth method" approle```
* enable kubernetes auth ```vault auth enable kubernetes```
* enable pki engine ```vault secrets enable pki```
* enable aws secrets engine ```vault secrets enable aws```
* enable gcp secrets engine ```vault secrets enable gcp```
* enable db secrets engine ```vault secrets enable database```
* renew revoke creds ```vault read database/creds/recordsApp```
* lease extension ```vault write sys/leases/renew lease_id=<lease_id> increment=3600```
* lease lookup ```vault write sys/leases/lookup lease_id=<lease_id> ```
* revoke lease ```vault write sys/leases/revoke lease_id=<lease_id> ```

## Resources
* Most [FAQ Questions in the Pop Quiz](https://github.com/MattN-HB/hashivaultlabs/blob/main/guides-presentations/pop%20quiz)
* [Vault deployment Guide](https://learn.hashicorp.com/tutorials/vault/deployment-guide)
* [Vault Learn](https://learn.hashicorp.com/vault)
* [Autounseal](https://learn.hashicorp.com/tutorials/vault/autounseal-transit)
* [Compare cloud kms](https://www.hashicorp.com/resources/how-vault-compare-cloud-kms)
* [App Integration](https://learn.hashicorp.com/tutorials/vault/eaas-spring-demo?in=vault/app-integration)
