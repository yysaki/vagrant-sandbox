# vagrant-sandbox

## How to install ansible

```
pyenv install 3.9.2
pyenv virtualenv 3.9.2 vagrant-sandbox
pip install -r < requirements.txt

vagrant up

# test
curl http://192.168.33.10:8080 # node1
curl http://192.168.33.11:8080 # node2
curl http://192.168.33.12:8080 # node3
```
