# Branching i merging

Git branches omogućavaju developer-ima da rade na raznim funkcijama, popravkama, ili eksperimentima nezavisno. U suštini, branch je pokretni pointer na commit.

---

## 1. Razumevanje branch-eva

Kao što smo rekli, glavni branch ćemo zvati main. Tipičan workflow:

![Example Git Branching Diagram](https://user-images.githubusercontent.com/1256329/117236177-33599100-adf6-11eb-967c-5ef7898b55dc.png)

*Hvala [poreklo slike](https://gist.github.com/bryanbraun/8c93e154a93a08794291df1fcdce6918)*

Izmene je moguće praviti nezavisno i merge-ovati kasnije.

U daljem tekstu branch ćemo zvati grana.

---

## 2. Pravljenje i menjanje grana

### Izlistavanje svih grana

```bash
git branch
```

Ako želimo da izlistamo i remote grane:

```bash
git branch -a
```

### Povratak na glavnu granu

```bash
git switch main
```

### Ažuriranje main-a

```bash
git pull
```

### Pravljenje i skok na novu granu

```bash
git switch -c feature/my-thing
```

Ovde se sad radi sve što treba na novoj grani (add, commit, itd.).

### Prvi push grane

```bash
git push -u origin feature/my-thing
```

Kasniji push-evi

```bash
git push 
```

### Običan skok na neku granu 

```bash
git switch other-branch 
```

### Ako želimo da preimenujemo granu na kojoj se trenutno nalazimo

```bash
git branch -m novo-ime 
```

---

## 3. Upravljanje granama

### Brisanje merge-ovane grane

```bash
git branch -d feature/my-thing
```

### "Nasilničko" brisanje

```bash
git branch -D feature/my-thing 
```

**Upozorenje:** "Nasilničko" brisanje može da odbaci commit-ove koji još nisu merge-ovani.

### Brisanje remote grana

```bash
git push origin --delete feature/my-thing 
```

**git-checkout** i dalje radi za menjanje i pravljenje grana, ali **switch/restore** su savremeni ekvivalenti.

### Ažuriranje referenci remote grana

```bash
git fetch --prune
```

## 4. Merge-ovanje grana 

Merge-ovanje kombinuje izmene iz jedne grane u drugu.

### Osnovni merge workflow

Prvo, prebacimo se na granu kojoj želimo da pridružimo izmene.

```bash
git switch main
```

Onda, merge-ujemo granu na kojoj smo radili.

```bash
git merge feature/my-thing
```

### Merge-ovanje bez fast-forward-a

```bash
git merge --no-ff feature/my-thing
```

Ovo pravi merge commit čak i kada je fast-forward merge moguć.

### Odustajanje od merge-a

```bash
git merge --abort
```

Ovo se koristi kada želimo da cancel-ujemo merge koji je u toku.

---

## 5. Bavljenje merge konfliktima

Merge konflikt se dešava kada dve grane izmene isti deo nekog file-a, pa Git ne može automatski da odluči koju verziju da zadrži.

### Provera konflikta

```bash
git status
```

### Otvaranje file-a koji pravi problem

Git može da pokaže nešto ovako: 

```text
<<<<<<< HEAD
This is the current branch version.
=======
This is the incoming branch version.
>>>>>>> feature/my-thing
```

### Rešavanje konflikta

Treba izmeniti file ručno i izabrati tačan sadržaj.

### Stage-ovanje popravljenog file-a

```bash
git add filename
```

### Dovršavanje merge-a

```bash
git commit
```

---

## 6. Rebase grana

Ako vas zanima možete da pročitate o rebase-ovanju na sledećem linku: [git rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing).

### Osnovni rebase

```bash
git switch feature/my-thing
git rebase main
```

### Nastavak nakon rešavanja konflikata

```bash
git add filename
git rebase --continue
```

### Obustavljanje rebase-a

```bash
git rebase --abort
```

**Važno:** izbegavajte rebasing deljenih grana na kojima radi još ljudi, osim ako se tim ne složi oko tog workflow-a.

---

[Povratak na glavni cheat sheet](README.md)