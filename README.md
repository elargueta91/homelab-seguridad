# homelab-seguridad

Documentación de un homelab doméstico de ciberseguridad diseñado para **detectar, contener y erradicar intrusiones** en una red que fue comprometida previamente. El proyecto combina segmentación por VLANs, monitoreo de red, EDR y respuesta ante incidentes.

## Objetivos

- Erradicar una intrusión persistente a través del módem ISP.
- Segmentar la red con VLANs para aislar IoT, invitados y dispositivos de confianza.
- Monitorear el tráfico interno y externo con Suricata (IDS).
- Detectar MAC spoofing con `arpwatch` y DAI.
- Centralizar logs y alertas con Wazuh (SIEM + EDR).
- Documentar todo el proceso como caso real de defensa.

## Arquitectura General

Internet
│
Módem ISP (VLAN 99)
│
Switch TL-SG2008 ─── Router Omada ─── AP Omada (WiFi)
│
├── Raspberry Pi (VLAN 40) → Suricata, Wazuh, arpwatch, Tailscale
└── PCs (VLAN 10) → Wazuh Agent, hardening


## Segmentación (VLANs)

| VLAN | Nombre     | Subred          | Uso                              |
|------|------------|-----------------|----------------------------------|
| 1    | Management | 192.168.1.0/24  | Router, switch, AP               |
| 10   | Trusted    | 192.168.10.0/24 | PCs, celulares personales        |
| 20   | IoT        | 192.168.20.0/24 | TVs, bombillas, enchufes, hub    |
| 30   | Guest      | 192.168.30.0/24 | Invitados                        |
| 40   | Mgmt RPi   | 192.168.40.0/24 | Raspberry Pi                     |
| 99   | WAN        | 192.168.0.0/24  | Módem ISP (solo transporte)      |

## Medidas de seguridad implementadas

- [x] Segmentación por VLANs con ACLs entre ellas.
- [x] Aislamiento de VLAN IoT y Guest (ACLs + Client Isolation).
- [x] SPAN del puerto del AP Omada para monitoreo con Suricata.
- [x] `arpwatch` en la VLAN del módem con alertas a Telegram.
- [x] Script de escaneo WAN con `nmap` y alertas a Telegram.
- [x] Firewall `iptables` en la Raspberry Pi (DROP por defecto).
- [x] Protección de `eth2` (sin gateway, sin DNS, sin servicios).
- [x] Fan control por temperatura con overlay `gpio-fan`.
- [ ] DHCP Snooping + Dynamic ARP Inspection (DAI) en el switch.
- [ ] Wazuh (SIEM + EDR).
- [ ] RADIUS + certificados EAP-TLS.
- [ ] Tailscale (Exit Node + Subnet Router).
- [ ] Pi-hole (DNS sinkhole).

## Estructura del repositorio

| Carpeta | Contenido |
|---------|-----------|
| `01-incidente` | Detección, evidencia y erradicación de la intrusión |
| `02-arquitectura` | Diagrama de red, VLANs y dispositivos |
| `03-configuraciones` | Configuración de switch, router, Raspberry y Suricata |
| `04-seguridad` | ACLs, DAI, arpwatch, script de escaneo WAN |
| `05-scripts` | Scripts utilizados en el homelab |
| `06-pendientes` | Roadmap de implementaciones futuras |
| `07-lecciones` | Aprendizajes y lecciones del proyecto |

## Nota sobre sanitización

Toda la información sensible (IPs públicas, MACs reales, tokens, contraseñas) ha sido **sanitizada** antes de publicarse en este repositorio.

## Licencia

MIT
