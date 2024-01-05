Vagrant.configure("2") do |config|

  # AD server.
  config.vm.define "ad_server" do |srv|
    srv.vm.box = "luminositylabsllc/bento-rockylinux-9-aarch64"
    srv.ssh.insert_key = false
    srv.vm.synced_folder ".", "/vagrant", type: "rsync",
      rsync__exclude: ".git/"
    srv.vm.provider "parallels" do |prl|
      prl.memory = 4096
      prl.linked_clone = true
    end
    srv.vm.hostname = "ad.test"
    srv.vm.network :private_network, ip: "192.168.56.10"
  end

  # Application server.
  config.vm.define "aduser1" do |app|
    app.vm.box = "luminositylabsllc/bento-ubuntu-20.04-arm64"
    app.ssh.insert_key = false
    app.vm.synced_folder ".", "/vagrant", type: "rsync",
      rsync__exclude: ".git/"
    app.vm.provider "parallels" do |prl|
      prl.memory = 2048
      prl.linked_clone = true
    end
    app.vm.hostname = "aduser1.test"
    app.vm.network :private_network, ip: "192.168.56.11"
  end

end