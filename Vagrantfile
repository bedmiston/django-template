# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'
DOCKER_HOST_NAME = "dockerhost"
DOCKER_HOST_VAGRANTFILE = "./DockerHostVagrantfile"

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

ENV['VAGRANT_DEFAULT_PROVIDER'] ||= 'docker'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "postgres" do |postgres|
    postgres.vm.provider 'docker' do |d|
      d.image  = 'abevoelker/postgres'
      d.name   = 'djangoapp_postgres'
      d.ports  = ['5432:5432']
      d.vagrant_machine = "#{DOCKER_HOST_NAME}"
      d.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"
    end
  end

  config.vm.define "djangoapp" do |djangoapp|
    djangoapp.vm.provider 'docker' do |d|
      d.build_dir = "."
      d.name            = 'djangoapp_web'
      d.ports           = ['8080:8080']
      d.vagrant_machine = "#{DOCKER_HOST_NAME}"
      d.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"

      d.link('djangoapp_postgres:postgres')
    end

    djangoapp.vm.synced_folder ".", "/var/www" #, owner: 'web', group: 'web'
  end
end
