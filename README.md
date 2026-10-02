# P2 – Infra 2: VPN Site-to-Site FortiGate ↔ MikroTik
**Gregorys Morel Duluc – 2025-0035 – Seguridad de Redes (ITLA)**

## Topología
FG1 (usuarios) ⇄ ISP 200.35.0.0/24 ⇄ MT1 – MikroTik CHR 6.49.17 (servidor).
Se usó MikroTik por no disponer de imagen Cisco.

## Plan de IPs
| Equipo | WAN | LAN |
|---|---|---|
| FG1 | 200.35.0.1/24 | 10.0.35.129/25 (VLAN 10, DHCP) |
| MT1 | 200.35.0.3/24 | 10.0.35.1/28 |
| Servidor web HTTPS | — | 10.0.35.2/28 |

## Configuración
- FG1 (GUI): VPN IPsec IKEv1, DES/SHA1, DH14, PFS.
- MT1: perfil, propuesta, peer, política IPsec, ruta a la red de usuarios y NAT (masquerade con excepción para el tráfico VPN).

## Pruebas
- `ping` y `curl -k https://10.0.35.2` desde PC1 por el túnel.
- `/ip ipsec active-peers print` → established.
- Túnel deshabilitado → curl falla; habilitado → funciona.

## Archivos
`FG1-Infra2.conf`, `MT1-Infra2.rsc`
