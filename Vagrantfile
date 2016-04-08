# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.vm.provider 'virtualbox' do |vb|
    vb.memory = '2048'
  end

  config.vm.synced_folder './share', '/home/vagrant/share', create: true

  config.vm.provision 'shell', privileged: false, inline: <<-SHELL
    # change to use JAIST mirror server
    if grep '//ftp.jaist.ac.jp/pub/Linux' /etc/apt/sources.list
    then
      echo 'already used JAIST mirror server'
    else
      sudo sed -i.bak -e 's|//archive.ubuntu.com|//ftp.jaist.ac.jp/pub/Linux|' /etc/apt/sources.list
    fi

    # update
    sudo apt-get update
    sudo apt-get --yes upgrade

    # install dependencies for blockdiag
    sudo apt-get --yes install python-setuptools python-imaging fonts-takao

    # install blockdiag family
    sudo easy_install blockdiag seqdiag actdiag nwdiag

    # create config file
    echo '[blockdiag]'                                                        >> $HOME/.blockdiagrc
    echo 'fontpath = /usr/share/fonts/truetype/takao-gothic/TakaoPGothic.ttf' >> $HOME/.blockdiagrc
    echo ''                                                                   >> $HOME/.blockdiagrc
    echo '[seqdiag]'                                                          >> $HOME/.blockdiagrc
    echo 'fontpath = /usr/share/fonts/truetype/takao-gothic/TakaoPGothic.ttf' >> $HOME/.blockdiagrc
    echo ''                                                                   >> $HOME/.blockdiagrc
    echo '[actdiag]'                                                          >> $HOME/.blockdiagrc
    echo 'fontpath = /usr/share/fonts/truetype/takao-gothic/TakaoPGothic.ttf' >> $HOME/.blockdiagrc
    echo ''                                                                   >> $HOME/.blockdiagrc
    echo '[nwdiag]'                                                           >> $HOME/.blockdiagrc
    echo 'fontpath = /usr/share/fonts/truetype/takao-gothic/TakaoPGothic.ttf' >> $HOME/.blockdiagrc
  SHELL
end
