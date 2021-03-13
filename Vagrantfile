# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version '>= 1.8.0'

N = 3
Vagrant.configure('2') do |config|
  config.vm.box = 'centos/8'

  (1..N).each do |node_id|
    config.vm.define "node#{node_id}" do |node|
      node.vm.hostname = "node#{node_id}"
      node.vm.network 'private_network', ip: "192.168.33.#{10 + node_id - 1}"
    end
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.groups = { 'all:vars' => { 'stage' => 'dev' },
                       'apache' => %w[node1 node2 node3],
                       'apache_vhost' => ['node2'],
                       'ftpserver' => ['node3'],
                       'loop_users' => ['node1'] }
    ansible.host_vars = { 'node2' => { 'stage' => 'prod' },
                          'node3' => { 'stage' => 'prod' } }
    ansible.limit = 'all'
    ansible.playbook = 'playbook.yml'
    ansible.verbose = 'vv'
  end
end
