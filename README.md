DESCRIPTION
short_description: Finds Path MTU (PMTU) from Cisco IOS network devices
description:
- Tests reachability using ping from Cisco IOS device to a remote destination.
- To find path MTU the binary search algorithm is used.
- The range of search of PMTU is between ( max_size - max_range) and ( max_size ).
author:
- Vladimir Krapovnitskiy (@vovilla)
extends_documentation_fragment:
- cisco.ios.ios
options:
  dest:
    description:
    - The IP Address or hostname of the remote node.
    required: true
    type: str
  max_size:
    description:
    - Max size of packets to send.
    type: int
  max_range:
    description:
    - Range of pmtu to check (power of 2).
    type: int
  source:
    description:
    - The source IP Address or interface.
    type: str
  vrf:
    description:
    - The VRF to use for forwarding.
    type: str

EXAMPLES
- name: Test reachability to 10.10.10.10 using default vrf
  cisco.ios.ios_pmtu:
    dest: 10.10.10.10

- name: Test reachability to 10.20.20.20 using NOC vrf
  cisco.ios.ios_pmtu:
    dest: 10.20.20.20
    vrf: NOC

- name: Test reachability to 10.40.40.40 using NOC vrf and setting source
  cisco.ios.ios_pmtu:
    dest: 10.40.40.40
    source: Loopback 0
    vrf: NOC

RETURN
pmtu:
  description: Show the pmtu.
  returned: always
  type: int
  sample: 1600