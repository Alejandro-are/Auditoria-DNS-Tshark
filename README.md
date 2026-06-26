# 🕵️‍♂️ Auditoría de Navegación y Análisis de Peticiones DNS

Este proyecto demuestra un ejercicio práctico de **Análisis de Red** realizado en un entorno controlado con **Kali Linux**. El objetivo fue capturar el tráfico y auditar la "libreta de contactos" (DNS) de la computadora para entender qué páginas se visitan y qué conexiones ocultas ocurren en segundo plano.

---

## 🚀 Comandos Utilizados

1. **Captura del tráfico:** Guardé toda la actividad de la red en un archivo llamado `detective.pcap`:
   ```bash
   sudo tshark -i eth0 -w /tmp/detective.pcap
   ```

2. **Filtro de Auditoría:** Aislé únicamente las preguntas de nombres de dominio (DNS) que hizo mi computadora:
   ```bash
   tshark -r /tmp/detective.pcap -Y "dns.flags.response == 0" -T fields -e ip.src -e dns.qry.name | head -n 20
   ```

---

## 📊 Resultados y Hallazgos Forenses

Al analizar las conexiones generadas por la dirección IP de mi laboratorio (`172.16.119.129`), se clasificaron los hallazgos en dos categorías:

### 1. Actividad de Usuario (Navegación Visible)
Se detectó el acceso legítimo a plataformas educativas y herramientas de ciberseguridad:
*   `www.udemy.com` (Plataforma de aprendizaje)
*   `www.netacad.com` (Academia de redes de Cisco)
*   `www.shodan.io` (Buscador de dispositivos e infraestructura)

### 2. Actividad Automatizada (Segundo Plano)
El análisis reveló conexiones que el sistema operativo y las páginas web realizan de forma automática para funcionar correctamente:
*   `firefox.settings.services.mozilla.com`: El navegador Firefox verificando actualizaciones de su configuración interna.
*   `wire.shodan.io`: Conexión de soporte técnico necesaria para cargar las funciones interactivas del sitio Shodan.
*   `kit.fontawesome.com`: Petición externa para descargar los iconos gráficos y estilos visuales de las páginas web visitadas.

---

## 🎯 Conclusión

El ejercicio demuestra cómo las herramientas de análisis de red permiten auditar la privacidad y el comportamiento de un sistema operativo. En este caso, **no se detectaron conexiones maliciosas ni sospechosas**. Toda la actividad oculta corresponde al comportamiento estándar de los sitios web modernos y los servicios de mantenimiento del navegador Firefox.

---
*Laboratorio práctico de ciberseguridad para el desarrollo de habilidades en análisis forense digital.*

