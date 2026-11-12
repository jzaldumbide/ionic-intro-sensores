# SensorLab — Ionic Angular Standalone + acelerómetro

Proyecto de clase para explorar el acelerómetro (X, Y, Z), calcular la magnitud, detectar picos de movimiento y reconocer inclinaciones aproximadas. **No utiliza GPS.**

## Requisitos

- Node.js 20.19+ o 22.12+
- npm
- Android Studio y Android SDK para probar en Android
- Teléfono físico con acelerómetro

## Instalación

```bash
npm install
npm install @capacitor/motion
ionic serve
```
En el caso de utilizar 
```
npm i --force
```
, utilizarlo con cuidado

La interfaz se abre en el navegador, pero **la lectura del sensor requiere un entorno compatible**. En un ordenador puede no haber datos de movimiento.

## Ejecutar en Android

```bash
npm run build
npx cap add android
npx cap sync android
npx cap open android
```

Conecta el teléfono, habilita depuración USB y ejecuta desde Android Studio. Tras cambiar código web, repite `npm run build && npx cap sync android`.

## Estructura

```text
src/app/
├── app.component.ts
├── app.routes.ts
├── home/
│   ├── home.page.ts
│   ├── home.page.html
│   └── home.page.scss
└── services/
    └── sensor.ts
```

## Cómo funciona

- `SensorService`: crea y elimina el listener del plugin `@capacitor/motion`.
- `HomePage`: muestra los ejes X/Y/Z y la magnitud `sqrt(x*x+y*y+z*z)`.
- Cuando la magnitud supera 15 m/s², registra un evento; el intervalo mínimo entre eventos es 700 ms.
- El indicador de inclinación es orientativo: calibra los ejes y signos según tu dispositivo.

**Nota:** La aceleración reportada puede incluir gravedad; el contador no equivale a un podómetro real. No agites violentamente el dispositivo.

## Experimentos

1. Coloca el teléfono sobre una mesa y observa los valores.
2. Inclínalo lentamente y compara X, Y y Z.
3. Muévelo suavemente y observa la magnitud.
4. Ajusta el umbral de 15 m/s² en `home.page.ts` y compara resultados.
5. Mejora el detector para evitar falsos positivos.

## Solución de problemas

- **Sin lecturas en navegador:** utiliza un teléfono físico con la app nativa.
- **Permiso denegado:** revisa permisos de movimiento y reinicia la aplicación.
- **Error de dependencias:** verifica versiones de Node/npm y ejecuta `npm install` de nuevo.
- **No se actualiza la app Android:** ejecuta `npm run build && npx cap sync android`.

## Recursos

- https://ionicframework.com/docs
- https://capacitorjs.com/docs
- https://github.com/capacitor-community/motion

## Entrega sugerida

Repositorio GitHub con código fuente, README propio, capturas desde un dispositivo físico y breve explicación de los experimentos.
