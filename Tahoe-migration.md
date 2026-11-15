Per **macOS 26 Tahoe** con la **Intel AX201**, la scelta consigliata è [laobamac/itlwm](https://github.com/laobamac/itlwm/releases) (build `AirportItlwm-Tahoe`)**: ti dà l'interfaccia Wi-Fi nativa di macOS senza toccare il volume di sistema, senza disattivare SIP e senza dover riapplicare patch dopo ogni aggiornamento di macOS.

### Confronto rapido per Intel AX201 su Tahoe

| Caratteristica | `laobamac/itlwm` (Consigliato) | `kgp-macPro/AirportItlwm-Tahoe` (v2.0.0) |
| --- | --- | --- |
| **Root patch / OCLP** | **Nessuna** (sistema 100% integro e SIP attivo) | Richiede **OCLP-CustoMac 3.0+** + stack legacy Ventura |
| **Aggiornamenti macOS** | Plug & play (non si rompe agli update) | Devi riapplicare le root patch a ogni update di Tahoe |
| **Wi-Fi 6 (802.11ax)** | Sì (aggiungendo il boot-arg `itlwm_he=1`) | Sì, con Beamforming (`-itlwmhe -itlwmbf`) |
| **AWDL / AirPlay / AirDrop** | No (solo Wi-Fi standard; WPA2 e WPA2/WPA3 misto) | Sì **AirPlay e Screen Mirroring** (`awdl0`), ma **non** AirDrop |
| **AppleVTD (`DisableIoMapper`)** | Richiede `DisableIoMapper = True` (o drop DMAR) | Supporta AppleVTD attivo senza drop DMAR |

---

### Configurazione OpenCore con `laobamac/itlwm` su Tahoe

Quando preparerai la EFI per passare a Tahoe:

* Scarica dalle release di `[github.com/laobamac/itlwm](https://github.com/laobamac/itlwm)` il pacchetto specifico **`AirportItlwm-Tahoe`** (non usare quello di Sequoia perché hanno ABI diverse).
* Metti in `EFI/OC/Kexts` e abilita nel `config.plist` (`Kernel -> Add`) **solo `AirportItlwm.kext**`.
* Rimuovi o disabilita eventuali residui delle vecchie configurazioni: `itlwm.kext`, `IOSkywalk.kext`, `IO80211FamilyLegacy.kext`, `AMFIPass.kext` (se lo usavi solo per il Wi-Fi) e l'eventuale voce in `Kernel -> Block` per `com.apple.iokit.IOSkywalkFamily`.
* Imposta `Kernel -> Quirks -> DisableIoMapper = True` (oppure rimuovi la tabella ACPI `DMAR`).
* *(Opzionale)* Aggiungi `itlwm_he=1` ai `boot-args` se vuoi attivare il Wi-Fi 6; senza quel flag funziona comunque in Wi-Fi 5 (802.11ac) con la massima stabilità.

*(Valuta `kgp-macPro/AirportItlwm-Tahoe` solo se per te è indispensabile trasmettere lo schermo via **AirPlay** o se non puoi disattivare `AppleVTD` per altre periferiche PCIe).*
