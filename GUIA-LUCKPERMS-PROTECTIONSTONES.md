# Guía LuckPerms para ProtectionStones (1.21.x)

Esta guía te propone una estructura por rangos:

- `default`
- `helper`
- `mod`
- `admin`
- `developer`
- `owner`

También incluye para qué sirve cada permiso y ejemplos de comandos LuckPerms.

---

## ✅ ¿Hay permisos útiles para `default`?

Sí.  
El rango `default` puede tener permisos básicos para que los jugadores usen ProtectionStones normalmente sin acceso administrativo.

---

## 1) Rango `default` (jugador normal)

Permisos recomendados:

- `protectionstones.create`  
  Permite crear protección al colocar el bloque.
- `protectionstones.destroy`  
  Permite romper su propio bloque de protección.
- `protectionstones.unclaim`  
  Permite desproteger su región con comando.
- `protectionstones.info`  
  Ver info de su región.
- `protectionstones.view`  
  Ver visualmente bordes de su región.
- `protectionstones.home`  
  Ir al home de su región.
- `protectionstones.sethome`  
  Configurar home de su región.
- `protectionstones.tp`  
  Teletransporte por comandos de PS.
- `protectionstones.list`  
  Listar sus regiones.
- `protectionstones.count`  
  Ver cuántas regiones tiene.
- `protectionstones.name`  
  Renombrar región.
- `protectionstones.toggle`  
  Activar/desactivar colocación de PS.
- `protectionstones.members`  
  Gestionar miembros.
- `protectionstones.owners`  
  Gestionar owners compartidos.
- `protectionstones.flags`  
  Configurar flags de su región.
- `protectionstones.get` *(opcional)*  
  Obtener bloque de protección por comando.

---

## 2) Rango `helper` (soporte)

Hereda de `default` +:

- `protectionstones.info.others`  
  Ver info de regiones de otros.
- `protectionstones.view.others`  
  Ver bordes de regiones ajenas.
- `protectionstones.list.others`  
  Listar regiones de otro jugador.
- `protectionstones.count.others`  
  Contar regiones de otro jugador.

> Recomendación: no dar permisos destructivos o admin aquí.

---

## 3) Rango `mod` (moderación)

Hereda de `helper` +:

- `protectionstones.priority`  
  Cambiar prioridad de región.
- `protectionstones.region`  
  Comandos avanzados de región.
- `protectionstones.unclaim.remote` *(opcional)*  
  Desproteger regiones remotamente (usar con cuidado).
- `protectionstones.hide`
- `protectionstones.unhide`  
  Control de ocultar/mostrar bloques PS.

---

## 4) Rango `admin` (administración PS)

Hereda de `mod` +:

- `protectionstones.admin`  
  Permiso principal admin de ProtectionStones.
- `protectionstones.give`  
  Dar bloques PS a jugadores.
- `protectionstones.setparent`
- `protectionstones.setparent.others`  
  Manejo de jerarquías parent de regiones.
- `protectionstones.tax`  
  Comandos de impuestos.
- `protectionstones.buysell`  
  Sistema compra/venta si está habilitado.
- `protectionstones.merge`  
  Merge de regiones.

---

## 5) Rango `developer` (técnico)

Hereda de `admin` +:

- `protectionstones.superowner`  
  Bypass de ownership/permisos en regiones.

> Úsalo solo para staff técnico o debugging.

---

## 6) Rango `owner` (dueño del servidor)

Opción recomendada:

- `protectionstones.*`

Opción más segura:

- Heredar de `developer` + permisos específicos adicionales según tu política.

---

## Ejemplo de jerarquía LuckPerms

```text
default
  └─ helper
      └─ mod
          └─ admin
              └─ developer
                  └─ owner
```

---

## Comandos LuckPerms de ejemplo

### Crear grupos
```bash
/lp creategroup default
/lp creategroup helper
/lp creategroup mod
/lp creategroup admin
/lp creategroup developer
/lp creategroup owner
```

### Herencias
```bash
/lp group helper parent add default
/lp group mod parent add helper
/lp group admin parent add mod
/lp group developer parent add admin
/lp group owner parent add developer
```

### Permisos base para default
```bash
/ lp group default permission set protectionstones.create true
/ lp group default permission set protectionstones.destroy true
/ lp group default permission set protectionstones.unclaim true
/ lp group default permission set protectionstones.info true
/ lp group default permission set protectionstones.view true
/ lp group default permission set protectionstones.home true
/ lp group default permission set protectionstones.sethome true
/ lp group default permission set protectionstones.tp true
/ lp group default permission set protectionstones.list true
/ lp group default permission set protectionstones.count true
/ lp group default permission set protectionstones.name true
/ lp group default permission set protectionstones.toggle true
/ lp group default permission set protectionstones.members true
/ lp group default permission set protectionstones.owners true
/ lp group default permission set protectionstones.flags true
```

> Nota: Algunos paneles copian/pegan mejor sin espacio luego de `/`.  
> Si tu consola no acepta `/ lp`, usa `/lp`.

### Permiso total para owner
```bash
/lp group owner permission set protectionstones.* true
```

---

## Recomendaciones importantes

1. **No des `protectionstones.admin` a `default/helper`.**
2. **Prueba permisos por rango en un entorno de test** antes de producción.
3. Si usas multiserver (Bungee/Velocity), verifica contextos de LuckPerms (`server=...`).
4. Si quieres limitar cantidad de regiones por rango, usa nodos tipo:
   - `protectionstones.limit.<n>` (según config/plugin).

---

## Verificación rápida in-game

Con una cuenta de cada rango prueba:

- `/ps help`
- `/ps get` (si aplica)
- colocar bloque PS
- `/ps info`
- `/ps add <jugador>`
- `/ps flag` (solo donde corresponda)
- comandos admin (`/ps admin ...`) solo en admin+.

---

Si quieres, te preparo una **segunda versión** de esta guía con política **estricta** (menos permisos por rango) o **survival-friendly** (más utilidades para default).

# Despues de agregar el gui:
https://builtbybit.com/resources/protectionstones-gui-modern-eng-and-esp.86926/

Perms para pegar en LuckyPerms:
```text
commandprompter.use, deluxemenus.menu.ps_menu, servervariables.use, protectionstones.create, protectionstones.destroy, protectionstones.flags, protectionstones.hide, protectionstones.home, protectionstones.list, protectionstones.members, protectionstones.owners, protectionstones.sethome, protectionstones.unclaim, protectionstones.unhide, protectionstones.view
```
