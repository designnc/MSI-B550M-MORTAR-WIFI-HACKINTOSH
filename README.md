# EFI Hackintosh - MSI B550M MAG Mortar WiFi · Ryzen 5 3600X · RX 5500 XT

Esta es la configuración EFI que utilizo para correr **macOS Ventura** en mi equipo basado en AMD Ryzen. Está basada en OpenCore y preparada para sistemas AMD usando los parches necesarios.

## 🖥️ Especificaciones del Sistema

| Componente       | Modelo                                     |
|------------------|--------------------------------------------|
| Placa madre      | MSI B550M MAG Mortar WiFi                  |
| Procesador       | AMD Ryzen 5 3600X (6 núcleos / 12 hilos)   |
| GPU              | ASUS Dual Radeon RX 5500 XT EVO 8GB        |
| RAM              | 32GB Corsair Vengeance RGB PRO DDR4 3600MHz|
| SSD (macOS)      | Corsair MP600 1TB NVMe                     |
| Refrigeración    | NZXT Kraken Z63 RGB                        |
| Gabinete         | Lian Li 011 Dynamic Razer Edition          |

## ✅ Funciona correctamente

- Gráficos acelerados por hardware
- Audio
- Ethernet
- Bluetooth (parcial)
- iServices (iCloud, App Store, iMessage, etc.)
- USB mapeado
- Boot sin USB

## ⚠️ No funciona / Requiere ajustes

- **WiFi interno**: No compatible (se recomienda adaptador USB o reemplazo de tarjeta).
- **CPU Core Count**: Es necesario ajustar manualmente los parches `Force cpuid_cores_per_package`.

---

## 🧠 Ajuste manual: Parcheo de núcleos AMD

Para un funcionamiento correcto en sistemas AMD, asegúrate de activar:

```
Kernel -> Quirks -> ProvideCurrentCpuInfo = true
```

Además, edita los parches de `algrey - Force cpuid_cores_per_package` en:

```
Kernel -> Patch -> 0  (para macOS 10.13, 10.14)
Kernel -> Patch -> 1  (para macOS 10.15, 11.0)
Kernel -> Patch -> 2  (para macOS 12.0+)
```

Reemplaza los siguientes valores según tu cantidad de núcleos reales:

| Núcleos reales | Hexadecimal | Ejemplo de Replace                |
|----------------|-------------|-----------------------------------|
| 6              | `06`        | `B8 06 00 00 00`, `BA 06 00 00 00`|
| 8              | `08`        | `B8 08 00 00 00`, `BA 08 00 00 00`|
| 12             | `0C`        | `B8 0C 00 00 00`, `BA 0C 00 00 00`|

**Para Ryzen 5 3600X (6 núcleos):**
```hex
B8 06 00 00 00
BA 06 00 00 00
BA 06 00 00 90
```

Puedes hacer esto desde **OpenCore Configurator**, **OC Auxiliary Tools** o manualmente en tu `config.plist`.

---

## 🧰 Recomendaciones

- Para mapear puertos USB desde Windows de forma fácil: [USBToolBox](https://github.com/USBToolBox/tool)
- Genera tu SMBIOS con [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- Siempre respalda tu EFI funcional antes de probar cambios

---

## 📥 Créditos

- OpenCore team  
- Dortania guide: https://dortania.github.io/OpenCore-Install-Guide/  
- algrey (parches CPUID AMD)  
- Comunidad Hackintosh-Latinoamérica  
