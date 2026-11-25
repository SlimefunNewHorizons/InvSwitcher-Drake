<!-- credits:start -->
> **Credits & license.** Port and maintenance by [JackStar6677-1](https://github.com/JackStar6677-1) and [DrakesCraft Labs](https://github.com/SlimefunNewHorizons). Original authors: [tastybento](https://github.com/tastybento), [BONNe](https://github.com/BONNe), [wellnesscookie](https://github.com/wellnesscookie). Upstream license: **Eclipse Public License 2.0** (see [LICENSE](LICENSE)). Details: [docs/UPSTREAM_ATTRIBUTION.md](docs/UPSTREAM_ATTRIBUTION.md) · Policy: [Rights & Attribution](https://github.com/SlimefunNewHorizons/.github/blob/main/RIGHTS_AND_ATTRIBUTION.md). Independent community project, not affiliated with or endorsed by the original authors or the official Slimefun team.
>
> **Créditos y licencia.** Port y mantenimiento por [JackStar6677-1](https://github.com/JackStar6677-1) y [DrakesCraft Labs](https://github.com/SlimefunNewHorizons). Autores originales: [tastybento](https://github.com/tastybento), [BONNe](https://github.com/BONNe), [wellnesscookie](https://github.com/wellnesscookie). Licencia original: **Eclipse Public License 2.0**. Detalle en [docs/UPSTREAM_ATTRIBUTION.md](docs/UPSTREAM_ATTRIBUTION.md).
<!-- credits:end -->

> **Branches / Ramas.** `main`: Paper/Purpur 1.21.11 (Java 21). `port-26x`: Paper/Purpur 26.x (production: Purpur 26.2, Java 25). If another section of this README says otherwise, this note prevails. / Si otra seccion de este README dice otra cosa, prevalece esta nota.

> [!WARNING]
> ### ⚠️ ARCHIVADO / CONSOLIDADO EN DRAKES-SUITES (`26.x`)
> Este repositorio ha sido consolidado de forma definitiva en el monorepo oficial:  
> 👉 [**Drakes-Suites v2.0.0-26.X (Suite 7: DrakesServer)**](https://github.com/SlimefunNewHorizons/Drakes-Suites)  
> Todo el desarrollo activo para Temporada 2 (**Purpur 26.2** / **Java 25**) se realiza exclusivamente allí.

<div align="center">

<img src="banner.svg" alt="InvSwitcher Drake Edition" width="100%">

# ✦ InvSwitcher · DrakesCraft Edition ✦

### Hardened 5-Modality Inventory, EnderChest, Health & XP Isolation Engine for Purpur 26.2 / Paper 1.21.x

[![RepoRanker](https://reporanker.com/badge/SlimefunNewHorizons/InvSwitcher-Drake)](https://reporanker.com/repos/SlimefunNewHorizons/InvSwitcher-Drake)
[![Purpur](https://img.shields.io/badge/Purpur-26.2_%2F_1.21.x-FFA000?logo=purpur)](https://purpurmc.org/)
[![Java](https://img.shields.io/badge/Java-21%2F25-ED8B00?logo=openjdk&logoColor=white)](https://openjdk.org/)
[![License](https://img.shields.io/badge/License-GPL--3.0-blue)](./LICENSE)
[![Zero-Leakage](https://img.shields.io/badge/Isolation-Zero--Leakage_5_Modes-10B981)](https://github.com/SlimefunNewHorizons/InvSwitcher-Drake)
[![Network](https://img.shields.io/badge/Network-DrakesCraft_Production-00E5FF)](https://web.drakescraft.cl)

**A hardened downstream fork of InvSwitcher for BentoBox on Purpur 26.2 / Paper 1.21.x, providing airtight cross-modality inventory isolation across DrakesCraft's 5 game modes with zero item smuggling and zero Data Components corruption.**

[🌐 Portal Oficial](https://web.drakescraft.cl) ·
[🛒 Tienda Oficial](https://drakescraft-v2.tebex.io) ·
[💬 Discord Oficial](https://discord.gg/rv3vtXZTk7) ·
[🏛️ Organización GitHub](https://github.com/SlimefunNewHorizons)

</div>

---

> ### 🏰 Comunidad Oficial de DrakesCraft
>
> * 🎮 **IP del Servidor (Java & Bedrock):** `mc.drakescraft.cl` *(Puerto Java: `25565`)*
> * 💬 **Discord Oficial:** [discord.gg/rv3vtXZTk7](https://discord.gg/rv3vtXZTk7)
> * 🌐 **Portal Web & Guía:** [web.drakescraft.cl](https://web.drakescraft.cl)
> * 🛒 **Tienda Oficial:** [drakescraft-v2.tebex.io](https://drakescraft-v2.tebex.io)

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
git clone https://github.com/SlimefunNewHorizons/InvSwitcher-Drake.git
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

This project is a sovereign fork maintained by [**JackStar6677-1**](https://github.com/JackStar6677-1) under [**DrakesCraft Labs**](https://github.com/SlimefunNewHorizons).

- **Original Project:** Created by the upstream authors and the open-source community.
- **DrakesCraft Optimizations:** Modernized for Paper/Purpur 1.21.11+, Java 21, high concurrency, asynchronous safety, and exploit/duplication prevention.
- **License:** Distributed under the original **GNU General Public License v3.0 (GPLv3)** (or original upstream license). See the [LICENSE](LICENSE) file for complete terms.
