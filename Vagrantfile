# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

ENV['VAGRANT_DEFAULT_PROVIDER'] ||= 'docker'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "postgres" do |postgres|
    postgres.vm.provider 'docker' do |d|
      d.image  = 'abevoelker/postgres'
      d.name   = 'djangoapp_postgres'
      d.ports  = ['5432:5432']
    end
  end

  config.vm.define "djangoapp" do |djangoapp|
    djangoapp.vm.provider 'docker' do |d|
      d.build_dir = "."
      d.name            = 'djangoapp_web'
      d.ports           = ['8000:8000']

      d.link('djangoapp_postgres:postgres')
    end

    #djangoapp.vm.synced_folder ".", "/var/www" #, owner: 'web', group: 'web'
  end
end
