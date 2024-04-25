Hide VM Status in Unraid:

https://forums.unraid.net/topic/90111-hide-os-vm-status/


Try adding this above </features> to see if it helps.
```
    <kvm>
      <hidden state='on'/>
    </kvm>
```
 

I know this is a very old post but I haven't seen this answered anywhere. I managed to run protected TeknoParrot games under a VM by editing the VM in XML view and adding the following inside the <domain> section:
```
  <qemu:commandline>
    <qemu:arg value='-cpu'/>
    <qemu:arg value='host,kvm=off,hv_vendor_id=null,-hypervisor'/>
  </qemu:commandline>
 ```



 
