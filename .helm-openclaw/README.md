kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.30/deploy/local-path-provisioner.ya

Also chage default path for Storage class

⏺ Talos enforces PodSecurity standards. The provisioner's helper pod needs hostPath access, which is blocked by the baseline policy.
                                                                     
  Label the namespace to allow privileged pods:                                                                                                  
                                                                                                                                                 
  kubectl label namespace local-path-storage pod-security.kubernetes.io/enforce=privileged --overwrite                                           
                                                                                                          