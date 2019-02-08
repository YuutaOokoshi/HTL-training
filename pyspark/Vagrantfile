Vagrant.configure("2") do |config|

    # 必要なプラグインを強制インストール
    unless Vagrant.has_plugin?('vagrant-s3auth')
        system('vagrant plugin install vagrant-s3auth') || exit!
        exit system('vagrant', *ARGV)
    end
    unless Vagrant.has_plugin?('vagrant-cachier')
        system('vagrant plugin install vagrant-cachier') || exit!
        exit system('vagrant', *ARGV)
    end
    unless Vagrant.has_plugin?('vagrant-hostmanager')
        system('vagrant plugin install vagrant-hostmanager') || exit!
        exit system('vagrant', *ARGV)
    end
    unless Vagrant.has_plugin?('vagrant-vbguest')
        system('vagrant plugin install vagrant-vbguest') || exit!
        exit system('vagrant', *ARGV)
    end

    #rootユーザーのパスワードは「vagrant」
    config.vm.box = "centos/7"

    config.vm.hostname = "local-htl-company"
    config.vm.network "private_network", ip: "192.168.8.18"
    
    # 以下プラグイン必須処理
    config.hostmanager.manage_host = true
    config.hostmanager.enabled = true
    config.cache.scope = :box 
    # ↑ここまで
    
    # ミドルウェアインストール
    config.vm.provision "yum", type: "shell" do |s|
        s.inline= <<-SHELL
            yum update -y

            yum install -y https://centos7.iuscommunity.org/ius-release.rpm
            yum install -y python36 python36u-pip
            
            ln -snf /usr/bin/pip3.6 /usr/bin/pip
        SHELL
    end
end