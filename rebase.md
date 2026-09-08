# Guía de Git Rebase

`git rebase` reescribe el historial de commits moviendo la base de tu rama actual a la punta de otra rama, creando una línea de tiempo lineal y limpia en tu proyecto.

## El Escenario
Creaste una rama `feature` a partir de `main`. Mientras escribías tu código, alguien más subió nuevos cambios a `main`. Ahora necesitas integrar esos cambios recientes en tu rama antes de fusionarla.

## Proceso de Rebase

### 1. Cambia a tu rama de trabajo
```bash
git checkout feature
```

### 2. Descarga la información más reciente del repositorio remoto
```bash
git fetch origin
```

### 3. Inicia el rebase contra la rama principal
```bash
git rebase origin/main
```
Git pondrá tus commits temporalmente en pausa, actualizará tu rama local con la versión más reciente de `main`, y luego volverá a aplicar tus commits uno por uno en la cima.

### 4. Resuelve conflictos (solo si es necesario)
Si hay choques en el código (por ejemplo, si tú y otro desarrollador modificaron la misma función en `main.rs`), Git detendrá el proceso. Deberás abrir los archivos, resolver el conflicto, marcarlos como resueltos y continuar:
```bash
git add main.rs
git rebase --continue
```
*(Si te equivocas o quieres cancelar todo el proceso, puedes usar `git rebase --abort`).*

### 5. Sube los cambios al repositorio remoto
Dado que el rebase reescribe el historial de commits, si tu rama `feature` ya existía en el servidor remoto, Git rechazará un push normal. Debes forzar la subida de manera segura:
```bash
git push --force-with-lease origin feature
```

