ansible チュートリアル
参考：http://yteraoka.github.io/ansible-tutorial/

node1からnode2にsshできるようにssh_keyを送る
$ vagrant ssh-config node1 > ssh_config
$ vagrant ssh-config node2 >> ssh_config
$ scp -F ssh_config ~/.vagrant.d/insecure_private_key node1:.ssh/id_rsa

疎通確認(node1 -> node2)
ansible -i hosts 192.168.33.12 -m ping

ssh_keyの設定が出来ず、毎回接続確認される場合は
/etc/ansible/ansible.cfgの以下の部分をFalseにする
  host_key_checking = False

遠隔からシェルの実行
ansible -i hosts test-servers -m shell -a "node -v"
test-serverの部分はipかhostsファイル内の定義名
