## **Shared Access and Medium Network Architecure**

# **Laboratory Session 4: Spanning Tree Protocol**

_Academic year 2023-2024_  
_Telematics Engineering Department - Universidad Carlos III de Madrid_

---

## Question 1
Explain the reason of this result.

> The bridges are not running STP, so the network is completely saturated with the bridges' Neighbor
> Advertisement NDP packets.

## Question 2
What is the main difference between this and the previous execution in question 1? Justify your answer.

> In this versions, the STP protocol prevents loops and ensures there is only one path from origin to
> destination, so the packet's propagation is limited and a connection is established correctly.

## Question 3
Which is the root bridge? How do you know that?

> The root bridge is, in my case, i09b1-1, with priority 32768 (default) and MAC 3A:A1:DA:3E:4E:4F. I know
> because in the "Root ID" description, instead of specifying a `root-path-cost`, the command sudo `ovs-appctl
> stp/show` states "This bridge is the root"

## Question 4
What is the role of the ports attached to the root bridge?

> All ports of the root bridge are Designated ports, in forwarding state.

## Question 5
What is the state of the ports attached to the root bridge?

> All ports on the root bridge are in Forwarding state

## Question 6
Which one is the new blocked port in the virtual topology?

> The blocked port in my case is i09b1-n1-e0 (the one we just set to cost 100). Its role is "alternate".

## Question 7
Show all necessary steps to set up these two VLANs if the following command is used to set up port e0 of switch1 as a VLAN based port with VLAN id equal to 100.

> 1. With all hosts still connected in the same LAN, use one host to ping all others (so they are stored in
> the forwarding table of the bridge).
> 2. Use the following command to show the learning table
>
>     ```# ovs-appctl fdb/show i<ID>-n0```
>
>     where `<ID>` is your particular bridge ID.
> 3. Go into each host's configuration to see their MAC address.
> 4. Identify the ports assigned to each host's MAC address: the ports assigned to host1 and host2's MAC
> addresses should use the VLAN ID 100, while the ports assigned to host3 and host4's MAC addresses should use
> the VLAN ID 200.
> 5. For each port, assign them a VLAN using the command
>
>    ```#sudo ovs-vsctl set port i<ID>-n0-e<PORT> tag=<VLANID>```
>
>    where `<ID>` is your particular bridge ID, `<PORT>` is one less than the port number shown in with the
>    `fdb/show` command, and `<VLANID>` is replaced with the VLAN ID obtained in step 4.
