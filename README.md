# ansible-powermax-example
Sample playbooks to show the capabilities of Ansible modules for PowerMax
## Details
The examples in this repo take you gradually from the simplest task of creating a Storage Group to gradually evolve into a full blown Oracle cluster with 2 hosts
 - Step 1: Shows how to create create a Storage Group ("provision1.yml") and how to define other Storage Group properties such us compression and SLO ("provision2.yml"). Please refer to the official documentation for a full list of options available in the Storage Group modules. The official DellEMC repo for the PowerMax Ansible module is https://github.com/dell/ansible-powermax. Finally you can use the "deprovision.yml" file to destroy the Storage GRoup
 - Step 2: Shows how to create a volume in a Storage Group ("provision1.yml") and then how to extend it ("provision2.yml")
 - Step 3: After running the scripts in Step 2, it will be clear that passing all the Unisphere details clutters the YAML file. More importantly specifying the creadentials openly in the YAML file is not ideal either. In this step we show how to deal with those two issues by leveraging variables defined on external variable YAML files.
    + Additionally you can use "ansible-vault encrypt creds.yml" to encrypt the contents of the "creds.yml" file. If you do so you will need to pass the "--ask-vault-pass" parameter during invokation so that Ansible prompts you for the password to decrypt the "creds.yml" file
    + As explained in the documentation in order to deprovision a volume you need to specify the Volume ID instead of the Volume name. In order to achieve that we need to read the properties of the volume before we delete it in order to extract "VolumeId". That is shown in the "get_vol_id.yml" shown. Please note that the "deprovision.yml" deletes the Storage Group first and then the volume
 - Step 4: Shows a full-blown provisioning scenario for a 2-node Oracle cluster. All the credit for this script goes to Paul Martin. Paul publishes a lot of great PowerMax related content in https://rawstorage.wordpress.com/ 
 - Step 5: The first version of the Ansible modules for PowerMax includes the ability to manage snapshots. The playbook in this step shows an example of how to create a snapshot, link it to a Storage Group and create a Masking View so that it can be accessed. This workflow is very typical for PowerMax customers that need create development environments. Now with Ansible it can be integrated into a larger plabook that manages other aspects of the stack too. Kudos to Paul Martin for paving the way on this one as well
