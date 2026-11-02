
# SSH Setup — GitHub autentifikacija

SSH (Secure Shell) dozvoljava bezbedno povezivanje lokalnog računara na GitHub koristeći kriptografske parove ključeva.

Umesto unosa kredencijala iznova i iznova, SSH koristi privatni ključ i javni ključ za autentifikaciju.

---

## 1. Razumevanje SSH ključeva

SSH koristi dva ključa:

| Ključ | Namena |
|---|---|
| Privatni ključ | Ostaje bezbedno na vašem računaru |
| Javni ključ | Dodaje se na GitHub nalog |

**Jako je bitno da se nikada ne deli privatni ključ!**

---

## 2. Provera za postojećim SSH ključevima

### Izlistavanje postojećih SSH ključeva

```bash
ls -al ~/.ssh
```

Potražite fajlove kao što su:

```text
id_ed25519
id_ed25519.pub
```

File koji se završava na `.pub` je javni ključ.

Ako već postoji adekvatan ključ moguće je ponovno korišćenje umesto generisanje novog.

---

## 3. Generisanje novog ključa

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Kada iskoči prompt:

1. Pritisnite enter da prihvatite default lokaciju file-a.
2. Unesite bezbednu šifru.
3. Potvrdite šifru.

Ovo pravi dva file-a:

```text
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

---

## 4. Start SSH agenta

SSH agent vodi računa o ključevima i može da zapamti šifru.

### Start agenta (Git Bash / Linux / macOS)

```bash
eval "$(ssh-agent -s)"
```

### Dodavanje privatnog ključa

```bash
ssh-add ~/.ssh/id_ed25519
```

Na Windows-u može da se koristi i OpenSSH agent servis. Pogledati zvanični GitHub guide za Windows konfiguracije.

---

## 5. Dodavanje javnog ključa na GitHub

### Korak 1: kopiranje javnog ključa

Za Git Bash ili Linux:

```bash
cat ~/.ssh/id_ed25519.pub
```

Za Windows PowerShell:

```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub
```

Iskopirati ceo izlaz.

### Korak 2: otvoriti GitHub podešavanja

1. Ulogujte se na GitHub.
2. Kliknite profilnu sliku.
3. Otvorite podešavanja.
4. Izaberite SSH and GPG keys.
5. Kliknite New SSH key.

### Korak 3: dodavanje ključa

- Title: Šta god
- Key type: Authentication Key
- Key: Nalepite javni ključ

Kliknite Add SSH key.

---

## 6. Testiranje SSH konekcije

Pokrenite:

```bash
ssh -T git@github.com
```

Pri prvoj konekciji, SSH može da vas pita da verifikujete GitHub-ov host fingerprint.

Prihvatite ga samo nakon verifikovanja da se poklapa sa GitHub-ovim published fingerprint-om.

Uspešna konekcija prikazuje poruku koja je slična sledećoj:

```text
Hi USERNAME! You've successfully authenticated,
but GitHub does not provide shell access.
```

Ovo potvrđuje da SSH autentifikacija radi.

---

## 7. Korišćenje SSH URL-ova za GitHub repo-e

### Kloniranje korišćenjem SSH

```bash
git clone git@github.com:USERNAME/REPOSITORY.git
```

### Izmena postojećeg remote-a iz HTTPS u SSH

```bash
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

### Provera remote URL-a

```bash
git remote -v
```

### Push izmena korišćenjem SSH

```bash
git push
```

### Pull izmena korišćenjem SSH

```bash
git pull
```

---

## 8. SSH troubleshooting

### Permission denied (javni ključ)

```text
Permission denied (publickey).
```

Moguća rešenja:

1. Proverite da je javni ključ dodat na GitHub.
2. Uverite se da privatni ključ postoji.
3. Proverite da li je SSH agent učitao ključ.
4. Proverite konekciju ponovo.

### Provera učitanih SSH ključeva

```bash
ssh-add -l
```

### Dodajte ključ ponovo

```bash
ssh-add ~/.ssh/id_ed25519
```

### Testiranje SSH u debug modu

```bash
ssh -vT git@github.com
```

Ovo pruža detaljne informacije o konekciji.

---

## Zvanični izvori

- [Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Adding an SSH key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

---

[Povratak na glavni cheat sheet](README.md)
