Vagrant
=======

Vagrant es una herramienta para la creación y configuración de entornos virtualizados. En términos generales Vagrant ofrece una capa de abstracción y configuración sobre un motor/plataforma de virtualización.

## Ejercicio

```
vagrant box add devops devops.box
curl -o Vagrantfile https://raw.githubusercontent.com/nicopaez/devops/master/Vagrantfile
vagrant up
```

Una vez que haya terminado, navegar http://localhost:8080 y verifica la pantalla de bienvenida de Nginx.

Ejecutar vagrant ssh e inspeccionar el directorio /vagrant y crear un archivo.

```
vagrant ssh
cd /vagrant
echo "prueba" > file.xt
exit
```

Salir de la máquina y verificar la existencia del archivo file.txt


Docker
======


```
vagrant ssh
docker ps
```

```
docker images
docker run -p 8080:8080 jenkins
```

curl -o Dockerfile https://raw.githubusercontent.com/nicopaez/devops/master/Dockerfile

docker build -t pingapp .

docker run -p 4567:4567 -d pingapp

Puppet
======

puppet module install puppetlabs-postgresql
touch mymodule.pp
```
class { 'postgresql::globals':
  manage_package_repo => true,
  version             => '9.3',
  } ->
  class { 'postgresql::server': }

postgresql::server::db { 'mydb':
  user     => 'postgres',
  password => postgresql_password('postgres', 'postgres'),
}

postgresql::server::role { 'postgres':
  superuser     => true,
  password_hash => postgresql_password('postgres', 'postgres'),
}
```

Una vez completo podemos conectarnos usando psql -h localhost -U postgres -W y verificar la existencia de la base de datos mydb.


Ansible
=======

ansible-galaxy install tunght13488.java

```
# playbook.yml
- hosts: all
  roles:
     - tunght13488.java
```     

ansible-playbook -i "localhost," -c local playbook.yml

Ansible 2
=========


sudo ansible-galaxy install rvm_io.rvm1-ruby
sudo ansible-playbook -i "localhost," -c local playbook.yml

```
# pingapp-playbook.yml
- hosts: all
  roles:
     - rvm_io.rvm1-ruby

  vars:
    rvm1_rubies:
      - 'ruby-2.2.1'

  tasks:
    - name: add vagrant to root and rvm groups
      user: name=vagrant groups="vagrant,root,rvm"

    - name: grant permissions
      file: path=/usr/local/rvm/ mode="g=rw"

    - name: get app
      git: repo=https://github.com/nicopaez/pingapp.git dest=/home/vagrant/pingapp

    - name: solve app dependencies
      shell: bundle install
      args:
        chdir: /home/vagrant/pingapp
      
```     

Finalmente podemos ejecutar la aplicacion ejecutando ruby app.rb -o 0.0.0.0