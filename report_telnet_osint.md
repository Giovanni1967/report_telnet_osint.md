
# 🛰️ Report OSINT – Interazione Telnet su IP 45.56.126.27

## 📌 1. Contesto dell’analisi
- **Obiettivo**: Interazione con un host remoto via Telnet (porta 23)
- **Finalità**: Studio OSINT e comportamento honeypot
- **Strumenti**: `telnet`, `nmap`
- **Sistema locale**: Debian 12
- **Data**: 21 maggio 2025
- **Analista**: root@debian (utente: giovanni)

---

## 🌍 2. Informazioni generali sull’host

| Campo         | Valore                                                     |
|---------------|------------------------------------------------------------|
| IP            | `45.56.126.27`                                             |
| Hostname      | `45-56-126-27.ip.linodeusercontent.com`                    |
| Provider      | Linode LLC                                                 |
| Paese         | Stati Uniti (US)                                           |
| Porta aperta  | TCP/23                                                     |
| Servizio      | `Cowrie Honeypot telnetd`                                  |
| Tecnologie simulate | D-Link, NetComm, USR, DD-WRT, Asus, Tera-EP, BCM96848, ecc. |

---

## 🔎 3. Risultato scansione Nmap

```bash
nmap -p 23 -sV 45.56.126.27
```

```
PORT   STATE SERVICE VERSION
23/tcp open  telnet  Cowrie Honeypot telnetd
```

### Identificazione multipla nel banner:
- Dlink-Router login
- NetComm ADSL2+ Wireless Router
- DD-WRT v3.0 (Asus RT-AC5300)
- Tera-EP login
- USR-G809 login
- BCM96848

---

## 🔐 4. Tentativi di accesso Telnet

### Tentativo 1
```
telnet 45.56.126.27 23
→ Prompt: FG8102 login:
→ Risultato: Connection closed
```

### Tentativo 2
```
→ Prompt: BCM96848:
→ Login: admin
→ Password: admin
→ Risultato: Connection closed
```

### Tentativo 3 – Login riuscito (simulato)
```
→ Prompt: Tera-EP login: admin
→ Password: admin
→ Output:
The programs included with the Debian GNU/Linux system are free software
admin@<dnoqhusxhs>:~$ ls
→ Connection closed by foreign host
```

---

## 🧠 5. Interpretazione del comportamento

- Honeypot **accetta qualsiasi combinazione** e registra tutti i tentativi.
- L’ambiente simulato emula prompt realistici di router o sistemi embedded.
- Dopo pochi comandi (es. `ls`), **la sessione viene chiusa automaticamente** per evitare abusi.
- Il comportamento è 100% coerente con il framework **Cowrie**.

---

## 🛡️ 6. Sicurezza e legalità

| Azione                    | Legale | Etico |
|---------------------------|--------|-------|
| Connessione a porta Telnet aperta | ✅     | ✅    |
| Comandi base (`ls`, `whoami`)    | ✅     | ✅    |
| Upload exploit / virus            | ❌     | ❌    |
| Tentativi di intrusione reali     | ❌     | ❌    |

⚠️ Le sessioni sono registrate sul server remoto. Ogni input è tracciato dal gestore del honeypot.

---

## 🔒 7. Hash del file di log (esempio)

```bash
sha256sum interazione_telnet.log
```

Output atteso:
```
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855  interazione_telnet.log
```

---

## 📌 8. Conclusione

- `45.56.126.27` è **un honeypot Cowrie esposto pubblicamente**.
- L’ambiente simula sistemi noti per studiare l’interazione di attori potenzialmente ostili.
- L’analisi è avvenuta in un contesto **etico, passivo e osservativo**, utile per:
  - Studenti di cybersecurity
  - Ricercatori OSINT
  - Documentazione forense e intelligence tecnica

---

## 📎 Allegati suggeriti (per GitHub)

- `report_telnet_osint.md` (questo file)
- Screenshot della sessione Telnet
- Hash del log `.log` o `.pcap`
- Eventuale script Python per accesso automatizzato (opzionale)

---

## 🧰 Extra (opzionale): Script Python Telnet Read-Only

Se vuoi, richiedilo: posso fornirti uno script che si collega, registra l’output e chiude la sessione dopo alcuni secondi in sicurezza.

---
