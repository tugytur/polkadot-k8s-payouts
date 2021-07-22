# Polkadot-K8s-Payouts

A tool to deploy an utily that automatically claims your Kusama/Polkadot validator rewards in a Kubernetes cluster. 

## My on-chain Identity

ALESSIO (Validator on Polkadot): 16cdSZUq7kxq6mtoVMWmYXo62FnNGT9jzWjVRUg87CpL9pxP  
ALESSIO (Validator on Kusama): GaK38GT7LmgCpRSTRdDC2LeiMaV9TJmx8NmQcb9L3cJ3fyX

![identity](assets/identity.png)

## Related Projects

- https://github.com/ironoa/polkadot-k8s-monitor

## Table Of Contents

* [Requirements](#requirements)
* [Polkadot Payouts](#polkadot-payouts)
* [How To Configure the Application](#how-to-configure-the-application)
* [How To Deploy it Locally](#how-to-deploy-it-locally)
* [How To Deploy it in Production](#how-to-deploy-it-in-production)
* [Future Developments](#future-developments)

## Requirements
* kind (if you want to deploy it locally): https://kind.sigs.k8s.io/docs/user/quick-start/#installation
* kind requires Docker: https://docs.docker.com/get-docker/
* A Kubernetes cluster (if you don't want to use kind)
* kubectl: https://kubernetes.io/docs/tasks/tools/
* helmfile: https://github.com/roboll/helmfile#installation => brew install helmfile (on macOS)

## Polkadot Payouts
This project is particularly suited to be working in synergy with the [polkadot-k8s-monitor](https://github.com/ironoa/polkadot-k8s-monitor), and his goal is to automate the [payout claims](https://wiki.polkadot.network/docs/learn-simple-payouts) for your validators.

## How To Configure the Application

You can find a sample of the nodes related yaml config file [here](config/nodes.sample.yaml).  

```yaml
validatorsPolkadot:
- name: ALESSIO
  stashAccount: 16cdSZUq7kxq6mtoVMWmYXo62FnNGT9jzWjVRUg87CpL9pxP
validatorsKusama: 
- name: ALESSIO-0
  stashAccount: GaK38GT7LmgCpRSTRdDC2LeiMaV9TJmx8NmQcb9L3cJ3fyX
```

You can find a sample of the environment variables related file [file](config/env.sample.sh), meant to contain also your secrets and your passwords:

```sh
export KUSAMA_CLAIMER_PASSWORD='yourPassword'
export POLKADOT_CLAIMER_WALLET=`{"address":"xx","encoded":"xx","encoding":{"content":["pkcs8","sr25519"],"type":["scrypt","xsalsa20-poly1305"],"version":"3"},"meta":{"name":"xx","whenCreated":xx}}`
```

## How To Deploy it Locally
I'd reccomend to test first this approach 

```bash
git clone https://github.com/ironoa/polkadot-k8s-payouts.git
cd polkadot-k8s-payouts
cp config/env.sample.local.sh config/env.sh #create the default env config file
cp config/nodes.sample.yaml config/nodes.yaml #create the default nodes config file
#just the fist time

./scripts/deployLocal.sh
# just re trigger it to deploy configuration changes

#if you want to delete your local cluster
#./scripts/uninstallLocal.sh
```

## How To Deploy it in Production
First, connect yourself to your chosen kubernetes cluster.

```bash
git clone https://github.com/ironoa/polkadot-k8s-payouts.git 
cd polkadot-k8s-payouts
cp config/env.sample.complete.sh config/env.sh #create the default env config file
cp config/nodes.sample.yaml config/nodes.yaml #create the default nodes config file
#just the fist time

./scripts/deployProduction.sh
# just re trigger it to deploy configuration changes
```

## Future Developments
- [ ] Improve the documentation
- [ ] Youtube tutorials 