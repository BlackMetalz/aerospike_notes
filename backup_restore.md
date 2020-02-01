
# Backup
- Backup command, require astools installed

```
asbackup --host localhost --namespace ns_aes_test --directory /data/asbackup/ns_aes_test_today
```

- Best practice for backup:

```
asbackup --node-list 1.2.3.4:3000,5.6.7.8:3000 --namespace test --directory backup_2015_08_24
```
- With gzip

asbackup -l  1.2.3.4:3000,5.6.7.8:3000 -n test -o - | gzip > asbackup/location/test_3000_$(date -I).asb.gz


# Restore

```
asrestore --host localhost --directory ns_aes_test_today/ -n oldnamespace,newnamespace
```
Usage:

```
Usage: asrestore [OPTIONS]                                                  
------------------------------------------------------------------------------
 -V, --version        Print ASRESTORE version information.                    
 -O, --options        Print command-line options message.                   
 -Z, --usage          Display this message.                              
                                                  
 -v, --verbose        Enable verbose output. Default: disabled           
                                                                         
Configuration File Allowed Options                                         
----------------------------------                                             
                                        
[cluster]                                                          
 -h HOST, --host=HOST                                           
                      HOST is "<host1>[:<tlsname1>][:<port1>],..."
                      Server seed hostnames or IP addresses. The tlsname is
                      only used when connecting with a secure TLS enabled
                      server. Default: localhost:3000     
                      Examples:             
                        host1                                                              
                        host1:3000,host2:3000                                         
                        192.168.1.10:cert1:3000,192.168.1.20:cert2:3000                                                                        
 --services-alternate                                                                                                                          
                      Use to connect to alternate access address when the                                                                      
                      cluster's nodes publish IP addresses through access-address                                                              
                      which are not accessible over WAN and alternate IP addresses                                                             
                      accessible over WAN through alternate-access-address. Default: false.                                                    
 -p PORT, --port=PORT Server default port. Default: 3000                   
 -U USER, --user=USER User name used to authenticate with cluster. Default: none
 -P, --password                                                          
                      Password used to authenticate with cluster. Default: none
                      User will be prompted on command line if -P specified and no
                       password is given.                            
 --auth                           
                      Set authentication mode when user/password is defined. Modes are
                      (INTERNAL, EXTERNAL, EXTERNAL_INSECURE) and the default is INTERNAL.
                      This mode must be set EXTERNAL when using LDAP
 --tls-enable         Enable TLS on connections. By default TLS is disabled.
 --tls-cafile=TLS_CAFILE                                                  
                      Path to a trusted CA certificate file.              
 --tls-capath=TLS_CAPATH.        
                      Path to a directory of trusted CA certificates.
 --tls-protocols=TLS_PROTOCOLS
                      Set the TLS protocol selection criteria. This format
                      is the same as Apache's SSLProtocol documented at http
                      s://httpd.apache.org/docs/current/mod/mod_ssl.html#ssl  
                      protocol . If not specified the asrestore will use '-all
                      +TLSv1.2' if has support for TLSv1.2,otherwise it will
                      be '-all +TLSv1'.                                  
 --tls-cipher-suite=TLS_CIPHER_SUITE              
                     Set the TLS cipher selection criteria. The format is
                     the same as Open_sSL's Cipher List Format documented
                     at https://www.openssl.org/docs/man1.0.2/apps/ciphers.
                     html                                                      
 --tls-keyfile=TLS_KEYFILE              
                      Path to the key for mutual authentication (if
                      Aerospike Cluster is supporting it).      
 --tls-keyfile-password=TLS_KEYFILE_PASSWORD                      
                      Password to load protected tls-keyfile.              
                      It can be one of the following:                    
                      1) Environment varaible: 'env:<VAR>'
                      2) File: 'file:<PATH>'
                      3) String: 'PASSWORD'                                                
                      Default: none            
                      User will be prompted on command line if --tls-keyfile-password                                                          
                      specified and no password is given.                                                                                      
 --tls-certfile=TLS_CERTFILE <path>                                                                                                            
                      Path to the chain file for mutual authentication (if                                                                     
                      Aerospike Cluster is supporting it).                                                                                     
 --tls-cert-blacklist <path>                                                                                                                   
                      Path to a certificate blacklist file. The file should
                      contain one line for each blacklisted certificate.        
                      Each line starts with the certificate serial number
                      expressed in hex. Each entry may optionally specify      
                      the issuer name of the certificate (serial numbers are      
                      only required to be unique per issuer).Example:
                      867EC87482B2
                      /C=US/ST=CA/O=Acme/OU=Engineering/CN=TestChainCA                
 --tls-crl-check      Enable CRL checking for leaf certificate. An error                  
                      occurs if a valid CRL files cannot be found in
                      tls_capath.                                           
 --tls-crl-checkall   Enable CRL checking for entire certificate chain. An
                      error occurs if a valid CRL files cannot be found in
                      tls_capath.
[asrestore]                                                          
  -n, --namespace <namespace> 
                      The namespace to be backed up. Required.            
  -d, --directory <directory>                                               
                      The directory that holds the backup files. Required,    
                      unless -i is used.                                      
  -i, --input-file <file>                                                   
                      Restore from a single backup file. Use - for stdin.
                      Required, unless -d is used.
  -t, --threads                                                          
                      The number of restore threads. Default: 20.        
  -m, --machine <path>                                                     
                      Output machine-readable status updates to the given path,
                       typically a FIFO.
  -B, --bin-list <bin 1>[,<bin 2>[,...]]                           
                      Only restore the given bins in the backup.
                      Default: restore all bins.                  
  -s, --set-list <set 1>[,<set 2>[,...]]                                   
                      Only restore the given sets from the backup.       
                      Default: restore all sets.          
  --ignore-record-error                     
                      Ignore permanent record specific error. e.g AEROSPIKE_RECORD_TOO_BIG.
                      By default such errors are not ignored and asrestore terminates.
                      Optional: Use verbose mode to see errors in detail.                                                                      
  -u, --unique                                                                                                                                 
                      Skip records that already exist in the namespace;                                                                        
                      Don't touch them.                                                                                                        
  -r, --replace                                                                                                                                
                      Fully replace records that already exist in the                                                                          
                      namespace; don't update them.                        
  -g, --no-generation                                                           
                      Don't check the generation of records that already 
                      exist in the namespace.                                  
  -N, --nice <bandwidth>,<TPS>                                                    
                      The limits for read storage bandwidth in MiB/s and
                      write operations in TPS.
  -R, --no-records                                                                    
                      Don't restore any records.                                          
  -I, --no-indexes                                                  
                      Don't restore any secondary indexes.                  
  -L, --indexes-last                                                      
                      Restore secondary indexes only after UDFs and records
                      have been restored.
  -F, --no-udfs                                                      
                      Don't restore any UDFs.
  -w, --wait                                                              
                      Wait for restored secondary indexes to finish building.
                      Wait for restored UDFs to be distributed across the cluster.
 -T TIMEOUT, --timeout=TIMEOUT                                                
                      Set the timeout (ms) for commands. Default: 10000     
                                                                         
                                                  
Default configuration files are read from the following files in the given order:
/etc/aerospike/astools.conf ~/.aerospike/astools.conf                    
The following sections are read: (cluster asrestore include)               
The following options effect configuration file behavior                       
 --no-config-file                       
                      Do not read any config file. Default: disabled
 --instance <name>                                              
                      Section with these instance is read. e.g in case instance `a` is specified
                      sections cluster_a, asrestore_a is read.             
 --config-file <path>                                                    
                      Read this file after default configuration file.
 --only-config-file <path>                  
                      Read only this configuration file.                                  
