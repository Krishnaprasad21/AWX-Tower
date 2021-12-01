# AWX-Tower
AWX tower installation file and steps to perform 


subscription-manager repos --enable rhel-7-server-ansible-2.9-rpms --enable rhel-7-server-extras-rpms
echo "Redhat Repositary added"
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
echo "Docker Repositary added"
yum install -y ansible docker-ce docker-ce-cli containerd.io python3 python3-pip git libselinux-python3
systemctl start docker
systemctl enable docker
pip3.6 install -U pip
pip install docker docker-compose
echo "pip install completd"
wget https://github.com/ansible/awx/archive/refs/tags/17.1.0.zip
unzip 17.1.0.zip
sed -i '/admin_password=password/s/^# //g' /root/awx-17.1.0/installer/inventory
sed -i '/project_data_dir/s/^#//g' /root/awx-17.1.0/installer/inventory
echo "Modified inventory file content"
echo "AWX Installation started..."
ansible-playbook -i /root/awx-17.1.0/installer/inventory /root/awx-17.1.0/installer/install.yml -vv
echo "AWX Installation completed"
echo "Access the webpage of AWX by typing the IP address of the VM in base machine"
