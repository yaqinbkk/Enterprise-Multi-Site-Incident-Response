# Enterprise Multi-Site Incident Response

Design, configuration baseline and troubleshooting of a multi-site enterprise network in Cisco Packet Tracer, with five incident tickets diagnosed and resolved layer by layer.

**Full report:** [`docs/Enterprise_Multi-Site_Incident_Response.pdf`](docs/Enterprise_Multi-Site_Incident_Response.pdf) (23 pages: design, configuration, baseline verification, ticket resolution, lessons learned, appendices with running configurations)

## The network
- 20 devices: 10 Cisco 2911 routers, 2 Catalyst 3650 distribution switches, 8 Catalyst 2960 access switches
- A two-router headquarters core connecting four regional sites (A to D) through dedicated Edge routers
- OSPF area 0 backbone, one EIGRP autonomous system per region (AS 1 to 4), mutual redistribution on the Edge routers
- Region D: distribution pair with HSRPv2 and an LACP Port-channel; other regions use router-on-a-stick
- DHCP with DHCP snooping and Dynamic ARP Inspection, port security, DNS, syslog and NTP
- SSH-only management restricted by ACL; ACL policy between sites on the HQ and Edge routers

## Incident tickets
| Ticket | Symptom | Layer | Root cause |
|---|---|---|---|
| TK001 | Intermittent loss, duplicate IP warnings | 3 | HSRP version 1 against version 2 on DSW2 |
| TK002 | SRV2 unreachable from all sites | 2 | VLAN 40 missing from the trunk allowed list on ASW2 |
| TK003 | Region B isolated, neighbors up | 3 | No OSPF/EIGRP redistribution on Edge-R2 |
| TK004 | APIPA address in Region A | 2 | DHCP snooping did not trust the uplink on ASW1 |
| TK005 | Three ACL-related failures | 4 | Wrong direction, wrong port position, wrong address match |

Each ticket follows the same method: symptom, layer-by-layer elimination, root cause, fix and verification.

## Repository layout
| Path | Content |
|---|---|
| `docs/` | Full report (PDF) |
| `docs/ticket-reports/` | The five individual ticket reports (Word) |
| `lab/` | Packet Tracer project file (`.pkt`) |

## Running the lab
Open the `.pkt` file in Cisco Packet Tracer. Lab credentials are listed in the report appendix and are for this lab only.

## Author
Yannick HUE
