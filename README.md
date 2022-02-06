## Ansible install ที่ Master node (Control node)

### MacOS

#### ถ้ายังไม่มี homebrew ลง homebrew ก่อนครับ

https://brew.sh/index_th

จากนั้นใช้คำสั่ง

$ brew install ansible\
$ ansible --version

### Ubuntu

$ sudo apt update\
$ sudo apt install software-properties-common\
$ sudo add-apt-repository --yes --update ppa:ansible/ansible\
$ sudo apt install ansible\
$ ansible –version

## Ansible docs
https://docs.ansible.com/ansible/latest/index.html
## Ansible built-in collections
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html
## YAML lint ( yaml validator)
http://www.yamllint.com/
## YAML Online Editor
https://codebeautify.org/yaml-validator


## Presentation slides
https://docs.google.com/presentation/d/1YyZV-EsLiZQz5_64OsHpNIYsw8SMngfE6kwQYLBmJfY/edit?usp=sharing


## คำสั่งเบื้องต้นในการใช้งาน ansible
### เช็คการเชื่อมต่อระหว่าง master node & managed nodes ทั้งทมด (Ping)
$ ansible -i inventory.cfg all -m ping

ถ้าสำเร็จ จะเป็น SUCCESS สีเขียว

### เช็คความจุในหน่วย MB ของ managed nodes ทั้งทมด
$ ansible -i inventory.cfg all -a "free -m"

### Execute playbook => ansible-playbook [playbookname.yaml] -i [inventory.cfg]
$ ansible test_playbook.yaml -i inventory.cfg

### ทบทวนสั้นๆ
- มีเครื่อง server ขึ้นมาอย่างน้อย 1 เครื่อง (จาก cloud, vm, local machine ก็ได้ ลงเป็น ubuntu 20.04 lts ไว้) เพื่อทดสอบการ ssh
- ssh ไปที่เครื่องนั้น โดยการ ใช้ user root, password ของเครื่องนั้นๆ $ ssh root@xx.xx.xx.xx
- generate_keygen ฝั่ง master node เครื่องเรา เอาไปไว้ที่ ฝั่ง managed nodes
- หากยังเคย generate key ให้ใช้คำสั่ง"$ ssh-keygen -t rsa" จะได้ public key มา ให้ทำการ copy โดยใช้คำสั่ง $ cat ./ssh/id_rsa.pub จากนั้น copy ไว้
- ไปวางที่เครื่อง managed node โดยทำการ vi .ssh/authorized_keys จากนั้น save (vim จะใช้ :x ในการ save)
- ทดสอบการรันอีกครั้ง โดย ssh root@xx.xx.xx.xx ไปที่ managed node ครั้งนี้จะไม่ต้องใส่ password
- สร้าง Inventory file เพื่อทำการ config
- ทดสอบการเชื่อมต่อ master & managed node โดยการ ping
- สร้าง Playbook file เพื่อทำการ execute สิ่งที่เราต้องการ
