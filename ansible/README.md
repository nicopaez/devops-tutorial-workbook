
# install the java playbook
sudo ansible-galaxy install colstrom.java

# run the playbook
sudo ansible-playbook -i "localhost," -c local playbook.yml -vvvv

# on your host
open http://localhost:8080
