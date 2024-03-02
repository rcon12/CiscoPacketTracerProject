# CiscoPacketTracerProject
# The Objective along with the detailed instructions to this prject are in the CPT Rules for Project.pdf. Here I will be putting my answers in a coded based format to make it easier to read my work and how I did things step by step. Along with this will be the actual final project.pkt download where it shows the physical topology of the work that was completed here. 

# Task 1 

# Step 1 
255.255.255.224

# Step 2 
30 

# Step 3 
Subnet       NetAddr                   UsableRange                          Broadcast
1            172.16.10.0               172.16.10.1 - 172.16.10.30          172.16.10.31
2            172.16.10.32              172.16.10.33- 172.16.10.62          172.16.10.64
3            172.16.10.65              172.16.10.66 - 172.16.10.94         172.16.10.95
4            172.16.10.96              172.16.10.97 - 172.16.10.126        172.16.10.127
5            172.16.10.128             172.16.10.129 - 172.16.10.158       172.16.10.159
6            172.16.10.160             172.16.10.161 - 172.16.10.190       172.16.10.191
7            172.16.10.192             172.16.10.193 - 172.16.10.222       172.16.10.223
8            172.16.10.224             172.16.10.225 - 172.16.10.254       172.16.10.255

# Task 2. 
# Step 1
enable
  configure terminal
    vlan 10  
      name Management
    exit
    vlan 20 
      name Marketing
    exit
    vlan 30
      name Accounting
    exit
    vlan 100
      name Native 
    exit
  exit
exit

# Step 2 
enable 
  configure terminal 
    interface range fastethernet 0/1-10
      switchport mode access
      switchport access vlan 10
    exit
    interface range fastethernet 0/11-20
      switchport mode access
      switchport access vlan 20
    exit
    interface range fastethernet 0/21-24
      switchport mode access
      switchport access vlan 30
    exit
  exit
exit

# Step 3 
  # Only on S1
  enable 
    configure terminal 
      interface gigabitethernet 0/2
        switchport mode trunk
      exit
    exit
  exit
  # End only S1
  
  # Only on S2 
  enable 
    configure terminal 
      interface gigabitethernet 0/1
        switchport mode trunk
      exit
    exit
  exit
  # End only S2
 
# Step 4 
  enable 
    configure terminal 
      interface range fastethernet 0/1-24
        switchport nonegotiate 
      exit
    exit
  exit

# Task 3 
  
# Step 1 
    enable 
      configure terminal   
        interface gigabitethernet 0/0
          ip address 172.16.10.1 255.255.255.224
        exit
      exit
    exit

# Step 2 
  enable 
    configure terminal 
      interface gigabitethernet 0/1 
        ip address 172.16.10.33 255.255.255.224
      exit
    exit
  exit

# Step 3 
  # Only on R1 
    enable 
      configure terminal 
        interface Serial0/0/1
          ip address 172.16.10.65 255.255.255.224
        exit
      exit
    exit
  # End Only on R1 

  # Only on R2 
    enable 
      configure terminal   
        interface Serial0/0/0
          ip address 172.16.10.66 255.255.255.224
        exit
      exit
    exit
  # End Only on R2

# Step 4 
    # Only on R1
      enable 
        configure terminal   
          interface Serial0/0/0
            ip adddress 172.16.10.97 255.255.255.224
          exit
        exit
      exit 
    # End only on R1 

    # Only on R3 
      enable 
        configure terminal
          interface Serial0/0/0
            ip address 172.16.10.98 255.255.255.224
          exit
        exit
      exit

# Step 5
  # Only on R2
    enable 
      configure terminal 
        interface Serial0/0/1
          ip address 172.16.10.129 255.255.255.224
        exit
      exit
    exit
  # End of only on R2

  # Only on R3 
    enable
      configure terminal
        interface Serial0/0/1
          ip address 172.16.10.130 255.255.255.224
        exit
      exit
    exit
  # End of only on R3

# Task 4
# Steps 1-5 
  enable 
    configure terminal   
      interface gigabitethernet 0/0
        no shutdown
      exit
      interface gigabitethernet0/0.10
        encapsulation dot1q 10 
        ip address 172.16.10.161 255.255.255.224
      exit
      interface gigabitethernet0/0.20
        encapsulation dot1q 20
        ip address 172.16.10.193 255.255.255.224
      exit
      interface gigabitethernet0/0.30
        encapsulation dot1q 30 
        ip address 172.16.10.255 255.255.255.224 
      exit
    exit
  exit
  show ip interface brief 

  # Step 6 
    enable
      configure terminal 
        interface gigabitethernet0/1
          swithport mode trunk
          switchport trunk native vlan 100
        exit
      exit
    exit

  # Step 7 
    show interface trunk
    enable 
      write
    exit

 # Task 5 
  # Steps 1-4
    enable 
      configure terminal 
        interface range fastethernet 0/1-24
          swithcport mode access 
          switchport port-security 
          switchport port-security violation restrict 
          switchport port-security mac-address sticky 
          shutdown
        exit
        interface fastethernet 0/1
          no shutdown
        exit
        interface fastethernet 0/11
          no shutdown
        exit
        interface fastethernet 0/21
          no shutdown 
        exit
      exit
    exit

 # Task 6 
  # Step 1 
    enable 
      configure terminal 
        interface serial0/0/0
          no shutdown
        exit
        interface serial0/0/1
          no shutdown
        exit
      exit
    exit

  # Step 2
  # Only on R3 
    enable 
      configure terminal 
        interface gigabitethernet0/0
          no shutdown
        exit
        interface gigabitethernet0/1 
          no shutdown 
        exit
      exit
    exit
  # End only on R3 

  # Step 3 
  # Only on R1 
    enable 
      configure terminal 
        router ospf 1 
          router-id 1.1.1.1
          network 172.16.10.0 0.0.0.31 area 0
          network 172.16.10.32 0.0.0.31 area 0 
          network 172.16.10.64 0.0.0.31 area 0 
          network 172.16.10.96 0.0.0.31 area 0
          network 172.16.10.128 0.0.0.31 area 0 
          network 172.16.10.160 0.0.0.31 area 0
          network 172.16.10.192 0.0.0.31 area 0 
          network 172.16.10.224 0.0.0.31 area 0
        exit
      exit
    exit
  # End only on R1 
  # Only on R2 
  enable 
      configure terminal 
        router ospf 1 
          router-id 2.2.2.2
          network 172.16.10.0 0.0.0.31 area 0
          network 172.16.10.32 0.0.0.31 area 0 
          network 172.16.10.64 0.0.0.31 area 0 
          network 172.16.10.96 0.0.0.31 area 0
          network 172.16.10.128 0.0.0.31 area 0 
          network 172.16.10.160 0.0.0.31 area 0
          network 172.16.10.192 0.0.0.31 area 0 
          network 172.16.10.224 0.0.0.31 area 0
        exit
      exit
    exit
  # End only on R2 
  # Only on R3 
  enable 
      configure terminal 
        router ospf 1 
          router-id 3.3.3.3
          network 172.16.10.0 0.0.0.31 area 0
          network 172.16.10.32 0.0.0.31 area 0 
          network 172.16.10.64 0.0.0.31 area 0 
          network 172.16.10.96 0.0.0.31 area 0
          network 172.16.10.128 0.0.0.31 area 0 
          network 172.16.10.160 0.0.0.31 area 0
          network 172.16.10.192 0.0.0.31 area 0 
          network 172.16.10.224 0.0.0.31 area 0
        exit
      exit
    exit
# End only on R3 

# Step 4
# Only on R3 
  enable 
  configure terminal 
    router ospf 1 
      passive-interface gigabitethernet0/0
      passive-interface gigabitethernet0/1
    exit
  exit
exit
# End only on R3 
# Only on R1 
  enable 
    configure terminal   
      router ospf 1 
        passive-interface gigabitethernet0/0
      exit
    exit
  exit
# End only R1 

# Task 6 
# Step 5 
  show ip route ospf 

# Task 7 
# Steps 1-5
  enable 
    configure terminal 
      username Admin password ACDC1973
      line console 0 
        login local
      exit
      enable password beatles1960
      service password-encryption
      bannor motd #COMPUTER NETWORKING ROCKS#
    exit
  exit

# Task 8 
# STeps 1-4
  configure terminal 
    ip domain-name Cyber.com
    crypto key generate rsa general-keys modulus 1024 
    ip ssh version 2 
    line vty 0 15 
      login local 
      transport input ssh 
    exit
  exit
exit

# Task 9 
# Steps 1-3
  configure terminal 
    ip access-list extended 100
    exit 
    access-list 100 deny ip host 172.16.10.62 host 172.16.10.29
    access-list 100 permit ip any any 
    interface gigabitethernet 0/1 
      ip access-group 100 in
    exit
  exit
exit


  
  
