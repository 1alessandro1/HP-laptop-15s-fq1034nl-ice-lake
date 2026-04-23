Guida per sistemare il bluetooth con le cuffie su Parrot 7 + PipeWire

```markdown
# 🐧 Guida Risoluzione Audio Bluetooth su Parrot OS (PipeWire)

Questa guida riassume i passaggi per risolvere l'errore **"No audio endpoints registered"** e i problemi di connessione con cuffie Bluetooth (es. Soundcore P30i).

## 1. Architettura Audio
Parrot OS utilizza **PipeWire** come server audio moderno. Il componente che gestisce la creazione degli "endpoints" (le uscite audio) si chiama **WirePlumber**.

---

## 2. Comandi di Emergenza (Reset Rapido)
Se le cuffie sono connesse ma non senti nulla o i tasti volume non funzionano, esegui:

```bash
# Riavvia il "ponte" audio e il gestore dei profili
systemctl --user restart pipewire pipewire-pulse wireplumber

# Se il Bluetooth è bloccato (Error.Failed)
sudo rfkill unblock bluetooth
sudo systemctl restart bluetooth
```

---

## 3. Risoluzione "No Audio Endpoints"
Se il sistema non vede le cuffie come dispositivo di output, probabilmente mancano i moduli SPA per il Bluetooth.

1. **Installa i componenti necessari:**
   ```bash
   sudo apt update
   sudo apt install libspa-0.2-bluetooth pipewire-audio-client-libraries
   ```

2. **Pulisci la cache dei profili corrotti:**
   ```bash
   rm -rf ~/.local/state/wireplumber/*
   rm -rf ~/.config/pulse/*
   ```

3. **Riavvia i servizi:**
   ```bash
   systemctl --user restart pipewire wireplumber
   ```

---

## 4. Pairing Professionale via Terminale (`bluetoothctl`)
Se l'interfaccia grafica fallisce, usa il terminale per un accoppiamento pulito:

1. Entra nel tool: `bluetoothctl`
2. Accendi l'adattatore: `power on`
3. Rendi il PC visibile: `agent on` e `default-agent`
4. Metti le cuffie in pairing e scansiona: `scan on`
5. Quando trovi l'indirizzo (es. `34:09:C9:71:C6:4C`):
   ```bash
   pair [MAC_ADDRESS]
   trust [MAC_ADDRESS]
   connect [MAC_ADDRESS]
   ```

---

## 5. Glossario dei Codec (HSP/HFP)
Quando usi il microfono, puoi scegliere tra due codec nel pannello audio:
* **mSBC (Consigliato):** "HD Voice", qualità superiore (16kHz), voce naturale.
* **CVSD:** Standard legacy, qualità telefonica bassa (8kHz), ma più stabile su lunghe distanze o hardware vecchio.

---

## 6. Fix Tasti Volume (Fn)
Se i tasti Fn non rispondono dopo il passaggio a PipeWire:

1. Assicurati che il demone delle impostazioni sia attivo:
   - Vai in `Centro di Controllo` -> `Scorciatoie da tastiera`.
   - Rimappa i tasti "Aumenta/Abbassa volume" premendo fisicamente le combinazioni Fn.
2. Oppure forza il riconoscimento tramite pacchetto di compatibilità:
   ```bash
   sudo apt install pipewire-alsa
   ```

---

## 7. Troubleshooting Avanzato
Se l'adattatore Bluetooth dà errore `org.bluez.Error.Failed`:
* **Reset Hardware (Intel):**
  ```bash
  sudo modprobe -r btusb
  sudo modprobe btusb
  ```
* **Controlla i Log:**
  ```bash
  dmesg | grep -i bluetooth
  # oppure
  journalctl --user -f -u wireplumber
  ```
```

Puoi copiare questo testo in un file e tenerlo a portata di mano! 🚀
