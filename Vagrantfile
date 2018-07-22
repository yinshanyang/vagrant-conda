Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 16384
    vb.cpus = 3
  end

  # user: root
  config.vm.provision "shell", inline: <<-SHELL
    # miniconda: make directory
    mkdir -p /opt/conda
    chown vagrant /opt/conda
  SHELL

  # user: vagrant
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    # miniconda: download
    wget -q "https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh" -O miniconda.sh

    # miniconda: start installation process
    bash miniconda.sh -b -f -p /opt/conda

    # miniconda: link path
    echo 'PATH=/opt/conda/bin:$PATH' >> .profile

    # miniconda: cleanup
    rm miniconda.sh
  SHELL
end
