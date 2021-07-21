# hashivaultlabs
Recently, took great hands on course with [Hashi Vault](https://www.hashicorp.com/products/vault). This is to share the knowledge and lessons learned during it. All the commands from vault labs and [presentations directory ](https://github.com/MattN-HB/hashivaultlabs/tree/main/guides-presentations)as outlined in the [agenda](https://github.com/MattN-HB/hashivaultlabs/blob/main/guides-presentations/Vault%20Enterprise%20Academy%20Agenda%20-%203%20Day.pdf)

*Disclaimer most of the formatting is quick dumps with no clean-up so apologize ahead a time for lack of formatting. All tokens / keys stored in the commands are lab only and to show example.

## When use vault instead of aws secrets manager: 
* multicloud
* dynamic key generation
* on prem implentation

## How to store keys
* HSM
* Transit vault (best used in airgapped)
* KMS (aws or gcp) / [keybase](keybase.io)

## Important syntax
* when want login in vault server to have right privs via token ```vault login -method=token <admintoken>```
* when want login in vault server to have right privs via userpass ```vault login -method=userpass username=<username> password=<password>```
* write a secret as that user ```vault kv put kv/users/cary/bio lastname=Grant age=99 gender=male```
## Resources
* Most [FAQ Questions in the Pop Quiz](https://github.com/MattN-HB/hashivaultlabs/blob/main/guides-presentations/pop%20quiz)
* [Vault deployment Guide](https://learn.hashicorp.com/tutorials/vault/deployment-guide)
* [Vault Learn](https://learn.hashicorp.com/vault)
* [Autounseal](https://learn.hashicorp.com/tutorials/vault/autounseal-transit)
* [Compare cloud kms](https://www.hashicorp.com/resources/how-vault-compare-cloud-kms)
