# Erradicacion de la intrusion

## Acciones tomadas

1. Reset de fabrica del modem ISP (multiples veces).
2. Cambio de contrasenas de administrador y WiFi.
3. Desactivacion de WiFi, UPnP, WPS y administracion remota.
4. Aislamiento del modem en VLAN 99 (transporte WAN).
5. Solicitud de cambio de modem al ISP.
6. Implementacion de segmentacion por VLANs.

## Resultado

- El atacante ya no puede acceder a la red interna.
- El modem sigue aislado en su VLAN de transporte.
- Se implemento monitoreo continuo (Suricata, arpwatch, scan WAN).

## Lecciones aprendidas

- Los modems de ISP son dispositivos potencialmente hostiles.
- La segmentacion por VLANs es esencial para contener amenazas.
- El monitoreo pasivo y activo permite detectar retornos.
