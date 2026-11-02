# Git osnove

Git je DVCS (distributed version control system) koji prati promene fajlova i omogućava developer-ima da zajedno rade na projektima.

## 1. Proveri Git instalaciju

### Proveri Git verziju

Ispisuje verziju instaliranog Git-a.

```bash
git --version
```

Primer ispisa:

```text
git version 2.x.x
```

---

## 2. Git konfiguracija

### Postavljanje username-a i email-a

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Imenovanje glavnog branch-a

Git obično imenuje glavni branch master. Libtardi su se osetili uvređeno ovime, pa se često glavni branch preimenuje u main.

```bash
git config --global init.defaultBranch main
```

Neke Git komande otvaraju text editor, kao što je **git commit** bez **-m**, **git commit --amend**, **git rebase -i**, i merge-uju commit poruke. Ovo podešavanje tera Git da koristi VS Code za to. **--wait** flag je bitan jer govori **code** komandi da bude blokirana dok se ne zatvori file tab. Bez nje, **code** reaguje odmah, Git misli da je završeno praznom porukom i commit se prekida.

```bash
git config --global core.editor "code --wait" # opcinonalno
```

### Pregled svih konfiguracija

```bash
git config --list
```

### Generisanje SSH key

**-t ed25519** bira algoritam za key. Ed25519 je savremen, brz i bezbedan. Takodje je tip koji GitHub preporučuje.

**-C "you@example.com"** dodaje comment label na ključ. Pomaže pri kasnijoj identifikaciji ključa (ne utiče na rad kljuća).

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Treba da se iskopira sadržaj javnog key file-a (npr. pomoću **cat ~/.ssh/id_ed25519.pub**, kopirati ispis), pa na GitHub-u otići na Settings -> SSH and GPG keys -> New SSH key. Dati mu naziv koji vam se sviđa. GitHub sada može da prepozna bilo šta što je potpisano vašim ključem kao vaše.

### Testiranje konekcije

```bash
ssh -T git@github.com # - T znaci ne otvaraj interaktivni terminal
```

**Pažnja:** **--global** opcija primenjuje podešavanja na sve lokalne repozitorijume.

---

## 3. Upravljanje repozitorijumima

### Inicijalizacija novog repozitorijuma

Pravi novi Git repozitorijum u trenutnom direktorijumu.

```bash
git init 
```

### Kloniranje postojećeg repozitorijuma

Skida remote repozitorijum na kompjuter.

```bash
git clone <url> # kopira postojeci repozitorijum
git clone <url> folder-name
```

### Povezivanje lokalnog repozitorijuma sa GitHub-om (nakon pravljenja praznog repozitorijuma tamo)

```bash
git remote add origin git@github.com:USER/REPO.git
git remote -v
git push -u origin main
```

---

## 4. Petlja: edit, stage, commit

### Provera statusa repo-a

```bash
git status
```

### Prikaz promena izmedju commit-ova (unstaged)

```bash
git diff
```

### Prikaz promena izmedju commit-ova (staged)

```bash
git diff --staged
```

### Stage file-a

```bash
git add file.txt
```

Moguće je i stage-ovati sve (nije preporučljivo)

```bash
git add .
```

Moguće je i stage-ovati deo po deo umesto celog file-a ("hunk by hunk")

```bash
git add -p # --patch
```

### Commit izmena

```bash
git commit -m "Pera Zdera"
```

Moguće je iskombinovati dva koraka na sledeći način: 

```bash
git commit -am "msg"
```

**-a** automatski stage-uje svaki modifikovani ili izbrisani file koji Git već prati, a **-m "msg"** daje poruku commit-a direktno u komandi.

Može i da se ispravi zadnji commit umesto da se pravi novi 

```bash
git commit --amend -m "Bolji Pera Zdera"
```

---

## 5. Prikaz log-a i istorije

```bash
git log --oneline --graph --all  # Kompaktan prikaz
git show <commit>
```

---

## 6. Ispravka izmena

### Odbacivanje unstaged izmena

```bash
git restore file.txt
```

### Unstage

```bash
git restore --staged file.txt
```

### Poništavanje commit-a, izmene ostaju staged

```bash
git reset --soft HEAD~1
```

### Poništavanje commit-a, izmene ostaju unstaged

```bash
git reset --mixed HEAD~1
```

### Poništavanje commit-a i izmene se odbacuju (destruktivno)

```bash
git reset --hard HEAD~1
```

### Novi commit koji poništava pređašnji (originalni commit ostaje u istoriji, ništa se ne briše)

```bash
git revert <commit> 
```

### Pronalaženje "izgubljenih" commit-ova

"Izgubljeni" znači da nisu više dostupni preko branch-eva ili tag-ova, što znači da se više ne pojavljuju u **git log**, iako commit i dalje postoji u Git-ovoj bazi neko vreme.

```bash
git reflog
```

### Recover

```bash
git reset --hard <reflog-hash>
```

### Brisanje untracked file-ova

```bash
git clean -fd      
```

---

[Povratak na glavni cheat sheet](README.md)