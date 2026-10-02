> [!WARNING]
> ### ⚠️ ARCHIVADO / CONSOLIDADO EN DRAKES-SUITES
> Este repositorio ha sido consolidado de forma definitiva en el monorepo oficial:  
> 👉 [**Drakes-Suites (Suite 7: DrakesServer)**](https://github.com/DrakesCraft-Labs/Drakes-Suites)  
> Todo el desarrollo activo, optimizaciones del Ticker Engine, compatibilidad con Paper 1.21.11 y preparación para 26.X se realiza exclusivamente allí.

<div align="center">

<img src="banner.svg" alt="InvSwitcher Drake Edition" width="100%">

# ✦ InvSwitcher · DrakesCraft Edition ✦

### Hardened 5-Modality Inventory, EnderChest, Health & XP Isolation Engine for Paper/Purpur 1.21.11

[![RepoRanker](https://reporanker.com/badge/DrakesCraft-Labs/InvSwitcher-Drake)](https://reporanker.com/repos/DrakesCraft-Labs/InvSwitcher-Drake)
[![Minecraft](https://img.shields.io/badge/Minecraft-1.21.11-7C4DFF?logo=minecraft&logoColor=white)](https://papermc.io/)
[![Purpur](https://img.shields.io/badge/Purpur-1.21.11-FFA000?logo=purpur)](https://purpurmc.org/)
[![Java](https://img.shields.io/badge/Java-21%2F25-ED8B00?logo=openjdk&logoColor=white)](https://openjdk.org/)
[![License](https://img.shields.io/badge/License-GPL--3.0-blue)](./LICENSE)
[![Zero-Leakage](https://img.shields.io/badge/Isolation-Zero--Leakage_5_Modes-10B981)](https://github.com/DrakesCraft-Labs/InvSwitcher-Drake)
[![Network](https://img.shields.io/badge/Network-DrakesCraft_Production-00E5FF)](https://web.drakescraft.cl)

**A hardened downstream fork of InvSwitcher for BentoBox on Paper/Purpur 1.21.11, providing airtight cross-modality inventory isolation across DrakesCraft's 5 game modes with zero item smuggling and zero Data Components corruption.**

[🌐 Portal Oficial](https://web.drakescraft.cl) ·
[🎮 Jugar en Vivo](https://web.drakescraft.cl/play) ·
[💬 Discord Oficial](https://discord.gg/rv3vtXZTk7) ·
[🏛️ Organización GitHub](https://github.com/DrakesCraft-Labs)

</div>

---

> ### 🏰 ¡Únete a la Red Oficial de DrakesCraft!
>
> * 🎮 **IP del Servidor (Java & Bedrock):** `play.drakescraft.cl` *(Puerto Java: `25565` | Puerto Bedrock: `19132`)*
> * 💬 **Discord de la Comunidad:** [discord.gg/drakescraft](https://discord.gg/rv3vtXZTk7)
> * 🌐 **Sitio Web:** [web.drakescraft.cl](https://web.drakescraft.cl) · 🛒 **Tienda Oficial:** [web.drakescraft.cl/store](https://web.drakescraft.cl/store.html)

---

## 🙏 Reconocimiento y Agradecimientos a BentoBoxWorld

Queremos expresar nuestro más sincero y profundo agradecimiento a **tastybento** y a toda la **Comunidad de BentoBoxWorld** por haber creado y mantenido este add-on modular de gestión de inventarios. 

Este repositorio (`InvSwitcher-Drake`) es un fork downstream de fortificación y compatibilidad diseñado específicamente para cubrir las fronteras de aislamiento estricto de las 5 modalidades de **DrakesCraft**.

---

## 🌟 Fortificaciones de la Edición DrakesCraft

### 1. 🛡️ Cierre de la Fuga de Mundos No-Isla (`Zero-Leakage`)
* **Problema en Upstream:** InvSwitcher original ignoraba los cambios de mundo si ninguno de los dos mundos involucrados estaba registrado como una isla activa de BentoBox (`!addon.getWorlds().contains(from) && !addon.getWorlds().contains(to)`). Esto permitía que un jugador se teletransportara entre **Survival (`world`)** y **Clásico (`clasico`)** o **Laboratorio (`laboratorio`)** conservando sus ítems.
* **Solución Drake:** Se rediseñó `PlayerListener.onWorldEnter` para evaluar los **Storage Keys** de destino y origen. Si el jugador cambia de grupo de modalidad, se fuerza el guardado y la carga inmediata del inventario correspondiente, impidiendo cualquier contrabando de ítems entre mundos.

### 2. 🌐 Mapeo Nativo de las 5 Modalidades de DrakesCraft

| Modalidad | Grupo de Mundos | Storage Key Asignado | Aislamiento Activo |
| :--- | :--- | :--- | :--- |
| 🛡️ **Survival Principal** | `world`, `world_nether`, `world_the_end` | `world` | Inventario, EnderChest, XP y Vida |
| 📦 **OneBlock** | `oneblock_world`, `oneblock_world_nether`, `...` | `oneblock_world` | Inventario, EnderChest, XP y Vida |
| ☁️ **SkyBlock** | `bskyblock_world`, `bskyblock_world_nether`, `...` | `bskyblock_world` | Inventario, EnderChest, XP y Vida |
| 🌲 **Clásico Vainilla** | `clasico`, `clasico_nether`, `clasico_the_end` | `clasico` | Inventario, EnderChest, XP y Vida |
| 🧪 **Laboratorio** | `laboratorio` | `laboratorio` | Inventario, EnderChest, XP y Vida |

### 3. 💎 Integración con `BentoBox-Drake` (`Zero-Item-Loss`)
* Plena compatibilidad con la deserialización nativa de Data Components en Paper 1.21.11, protegiendo charms de Slimefun, armaduras personalizadas y armas con atributos al guardar o restaurar inventarios.

---

## 📦 Compilación e Instalación

### Compilar desde el Código Fuente
```bash
# Clonar el repositorio
git clone https://github.com/DrakesCraft-Labs/InvSwitcher-Drake.git
cd InvSwitcher-Drake

# Compilar con Maven (Java 21+)
mvn clean package
```

El binario se generará en `target/InvSwitcher-*.jar`.

### Instalación en el Servidor
1. Coloca `InvSwitcher.jar` en `/plugins/BentoBox/addons/`.
2. Asegúrate de tener `BentoBox.jar` (Edición Drake) en `/plugins/`.
3. Reinicia el servidor en la ventana de mantenimiento.

---

## 📄 License & Upstream Attribution

This project is a sovereign fork maintained by [**JackStar6677-1**](https://github.com/JackStar6677-1) under [**DrakesCraft Labs**](https://github.com/DrakesCraft-Labs).

- **Original Project:** Created by the upstream authors and the open-source community.
- **DrakesCraft Optimizations:** Modernized for Paper/Purpur 1.21.11+, Java 21, high concurrency, asynchronous safety, and exploit/duplication prevention.
- **License:** Distributed under the original **GNU General Public License v3.0 (GPLv3)** (or original upstream license). See the [LICENSE](LICENSE) file for complete terms.
