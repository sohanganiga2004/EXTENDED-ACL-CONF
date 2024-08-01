# EXTENDED-ACL-CONF

### Restrictions:
1. PC0 should not access Server1 (192.168.3.1) via HTTP.
2. Laptop0 should not ping Server1 (192.168.3.1).
3. PC1 should not access FTP on Server1 (192.168.3.1).

### Step-by-Step Configuration:

#### Step 1: Define the Extended ACL
1. **Access the CLI of the Router** where the ACL will be applied (assuming Router1 here).

#### Commands to Enter Global Configuration Mode:
```bash
enable
configure terminal
```

#### Define the ACL with Restrictions:
```bash
access-list 100 deny tcp host 192.168.1.1 host 192.168.3.1 eq 80
access-list 100 deny icmp host 192.168.1.2 host 192.168.3.1 echo
access-list 100 deny tcp host 192.168.2.1 host 192.168.3.1 eq 21
access-list 100 permit ip any any
```

#### Step 2: Apply the ACL to the Interface
Apply the ACL to the appropriate interface in the inbound direction.

#### Interface Configuration Example:
```bash
interface GigabitEthernet0/0
ip access-group 100 in
```

### Full Configuration Example:

1. **Access Router CLI:**
   ```bash
   enable
   configure terminal
   ```

2. **Create the Extended ACL:**
   ```bash
   access-list 100 deny tcp host 192.168.1.1 host 192.168.3.1 eq 80
   access-list 100 deny icmp host 192.168.1.2 host 192.168.3.1 echo
   access-list 100 deny tcp host 192.168.2.1 host 192.168.3.1 eq 21
   access-list 100 permit ip any any
   ```

3. **Apply the ACL to the Interface:**
   ```bash
   interface GigabitEthernet0/0
   ip access-group 100 in
   exit
   ```

### Verifying the Configuration
You can verify the ACL configuration by using the following commands:

```bash
show access-lists
show ip interface GigabitEthernet0/0
```

This will display the access list and its application on the interface, ensuring that the specified restrictions are applied correctly.

This configuration ensures that:
- PC0 (192.168.1.1) cannot access Server1 (192.168.3.1) via HTTP (port 80).
- Laptop0 (192.168.1.2) cannot ping Server1 (192.168.3.1).
- PC1 (192.168.2.1) cannot access FTP on Server1 (192.168.3.1).

