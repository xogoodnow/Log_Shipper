
<div align="center">
    <h1>Production Ready Log shipper</h1>
    <i>A Fluentbit implementation for production use in different modes</i>

</div>

### Components Used

| Name:Version         | Documentation                                                                                     | Purpose                                          | Alternatives                       | Advantages                                                                                                                                                                              |
|----------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ansible 2.15.2       | [Docs](https://docs.ansible.com/)                                                                 | Automating Tasks                                 | `Salt`                             | 1. No footprint on target hosts                                                                                                                                                         |
| Ubuntu  22.04        | [Docs](https://www.google.com/search?client=safari&rls=en&q=ubuntu+image+22.04&ie=UTF-8&oe=UTF-8) | Operating system                                 | `Debian` `Centos`                  | 1. Bigger community<br/>2. Faster releases than debian<br/>3. Bigger community than any other OS<br/>4. Not cash grapping like centos (Yet :))                                          |
| Fluentbit: 2.0.6     | [Docs](https://docs.fluentbit.io/manual)                                                                                                  | Log Collctor/Shipper                    | `Logstash` `fluentd`                            | 1. No seperate component for shipper and collector<br/>2. No extra dependency<br/>3. Very efficient (faster than fluentd)<br/>4. Almost zero foot print (Comparing to alternatives)<br/>5. Much easier to setup and manage<br/>6. Good number of useful plugins |
| Docker latest        | [Docs](https://docs.docker.com/)                                                                  | Application Deployment and Management            | `containerd` `podman`              | 1. Much more bells and wistels are included out of the box comparing to alternatives<br/>2. Awsome community and documentation <br/>3. Easy to work with                                |



## Before you begin
> **Note**
> Each ansible role has a general and a specific Readme file. It is encouraged to read them before firing off
> 
> p.s: Start with the readme file of main setup playbook
> First of all, fill out the all.yaml vars file based on your requirements
![image](https://s3.ir-thr-at1.arvanstorage.ir/kanglogshipper/log_shipper_vars_sample.png)


> Second fill out the inventory file (just put in the IP address and additional hosts if needed)

![image](https://s3.ir-thr-at1.arvanstorage.ir/kanglogshipper/log_shipper_inventory_sample.png)




## Work flow
* Run the following command for fire off the ansible on the given targets
``` bash
PWD='../'  ansible-playbook -i inventory.yaml Playbooks/Setup.yaml --private-key SSH_Keys/private_key.pem 
```
![image](https://s3.ir-thr-at1.arvanstorage.ir/kanglogshipper/log_shipper_ansible_run.gif)


* On the target node, check the logs for the container 
> **Note**
> Keep in mind that is tcp and udp mode, fluentbit patiently waits for your input as stream.
> This is for the tail mode (the container name might differ in your case, based on the index of node in the inventory)
``` bash
docker logs -f Fluentbit-tail-log_shipper_1-0
```
![image](https://s3.ir-thr-at1.arvanstorage.ir/kanglogshipper/log_shipper_tail_works.gif)

* Checking kibana to see if logs have been sent propely
> **Note**
> Some random auth log is being sent here for demonstartion purpose
![image](https://s3.ir-thr-at1.arvanstorage.ir/kanglogshipper/log_shipper_log_sent.gif)







