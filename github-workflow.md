# GitHub workflow

GitHub je cloud platforma za host-ovanje Git repozitorijuma. Dozvoljava developer-ima da čuvaju kod online, sarađuju, imaju uvid u izmene i upravljaju projektima.

---

## 1. Razumevanje remote repozitorijuma

Remote repozitorijum je verzija vašeg projekta host-ovana na platformi kao što je GitHub. Default remote ime je obično *origin*.

### Uvid u remote repozitorijume

```bash
git remote -v
```

### Dodavanje remote repozitorijuma

```bash
git remote add origin <repository-url>
```

### Izmena remote URL-a

```bash
git remote set-url origin <new-url>
```

### Uklanjanje remote-a

```bash
git remote remove origin
```

---

## 2. Povezivanje lokalnog repozitorijuma na GitHub

### Inicijalizacija, stage, commit

```bash
git init
git add . # preporučljivo da se radi file po file
git commit -m "inicijalni commit"
```

### Dodavanje GitHub remote-a

```bash
git remote add origin <repository-url>
```

### Promena imena grane na main

```bash
git branch -M main
```

### Push na GitHub

```bash
git push -u origin main # -u postavlja upstream granu kako bi budući push-evi koristili git push
```

---

## 3. Push-ovanje izmena na GitHub

### Push trenutne grane

```bash
git push
```

### Push određene grane

```bash
git push origin feature/my-thing
```

### Postavljanje upstream-a tokom push-ovanja

```bash
git push -u origin feature-login
```

**Uvek prvo commit-ujte izmene pre push-ovanja**

---

## 4. Pull-ovanje izmena sa GitHub-a

### Pull sa main-a

```bash
git pull origin main
```

### Pull sa praćene remote grane

```bash
git pull
```

### Pull korišćenjem [rebase](https://www.geeksforgeeks.org/git/when-to-use-git-pull-rebase/)

```bash
git pull --rebase
```

## 5. Fetch-ovanje izmena

Fetch skida informacije o remote izmenama bez integrisanja u trenutnu granu.

### Fetch svih remote novina

```bash
git fetch
```

### Fetch sa specifičnog remote-a

```bash
git fetch origin
```

### Fetch i uklanjanje obrisanih remote preferenci

```bash
git fetch --prune
```

---

## 7. Forking i cloning

Fork je sopstvena GitHub kopija tušeg repo-a.

### Kloniranje repo-a

```bash
git clone <repository-url>
```

### Dodavanje originalnog repo-a kao upstream

```bash
git remote add upstream <original-repository-url>
```

### Provera remote-ova

```bash
git remote -v
```

### Fetch novina iz originalnog repo-a

```bash
git fetch upstream
```

### Merge originalnog main-a u lokalni main

```bash
git switch main
git merge upstream/main
```

---

## 8. Rad sa remote granama

### Izlistavanje remote grana

```bash
git branch -r
```

### Izlistavanje svih grana

```bash
git branch -a
```

### Praćenje postojeće remote grane

```bash
git switch --track origin/feature/my-thing
```

### Brisanje remote grane

```bash
git push origin --delete feature/my-thing
```

---

## Zvanični izvori

- [GitHub Documentation](https://docs.github.com/)
- [GitHub Pull Requests](https://docs.github.com/en/pull-requests)
- [GitHub Skills](https://skills.github.com/)

---


[Povratak na glavni cheat sheet](README.md)