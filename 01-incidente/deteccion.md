# Deteccion de la intrusion

## Contexto

Tras varios cambios de seguridad en el modem ISP, se detecto que un dispositivo
desconocido se reconectaba automaticamente por WiFi tras cada reseteo de fabrica.

## Senales de alerta

- Dispositivo WiFi desconocido conectado tras reset.
- Cambio del rango de IP LAN sin intervencion del usuario.
- Persistencia tras cambio de contrasenas y reseteos.

## Evidencia

- Capturas del panel del modem (sanitizadas).
- Lista de dispositivos conectados.
- Logs del sistema (si disponibles).

## Conclusion

El modem ISP presentaba un backdoor a nivel de firmware/TR-069 que permitia
reconfigurarlo de forma remota, incluso tras reseteos de fabrica.
