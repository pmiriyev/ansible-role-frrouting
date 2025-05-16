================================
OpenStack-Ansible FRRouting role
================================

This role installs and configures FRRouting for providing support of dynamic
routing protocols, like BGP, OSPF, etc.

It is also used as a backend for `OVN BGP Agent <https://docs.openstack.org/ovn-bgp-agent/>`_
implementations.

To clone or view the source code for this repository, visit the role repository
for `frrouting <https://opendev.org/openstack/ansible-role-frrouting>`_.

Sample configuration
~~~~~~~~~~~~~~~~~~~~

.. code:: yaml

    frr_staticd_routes:
      - ip route 10.0.0.0/24 192.168.1.10
    frr_bgpd_config:
      - router bgp 1234
      - "bgp router-id 172.18.0.2"
      - "neighbor 172.18.0.3 remote-as 5678"
      - network 192.168.1.0/24
      - address-family ipv4 unicast
      - "  neighbor 172.18.0.3 prefix-list pl-allowed-adv out"
      - "exit-address-family"
      - ip prefix-list pl-allowed-adv seq 5 permit 192.168.1.0/24
      - ip prefix-list pl-allowed-adv seq 10 deny any

Default variables
~~~~~~~~~~~~~~~~~

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Example playbook
~~~~~~~~~~~~~~~~

.. literalinclude:: ../../examples/playbook.yml
   :language: yaml
