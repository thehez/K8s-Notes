## Security Contexts

Security contexts provide the ability to:
* Implement DAC - limit access based on group or user ID
* limit capabilities - confine root access to certain commands
* apply profiles - configure seccomp or use apparmor to restrict system calls
* Implement MAC - using SELinux to assign security labels to operating system objects.  

Example YAML: 

    Spec:
      securityContext:
        runasUser: 1000
        fsgroup: 2000
      Containers:
        security context:
          allowprivilegeEscalation: false
          
  ## Pod Security Policy
  
 A pod security policy (PSP) is a cluster-level resource that controls security sensitive aspects of a pods specification. the PSP objects define a set of conditions
 that a pod must run with in order to be accepted into the system, as well as providing defaults for related fields. 
