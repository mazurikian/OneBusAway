# Adaptación OneBusAway

Este proyecto parte de `OneBusAway-main` como base y conserva su estructura moderna de Android Studio:

- módulo `:app`
- `settings.gradle` con `pluginManagement` y `dependencyResolutionManagement`
- `gradle/libs.versions.toml`
- `build.gradle` raíz con `plugins { alias(...) apply false }`
- wrapper y configuración JDK/Gradle del proyecto nuevo

El código real, recursos, manifest, flavors, schemas, `google-services.json`, keystore debug y reglas ProGuard fueron incorporados desde el proyecto original `onebusaway-android` dentro del módulo `app`.

## Decisiones importantes

1. **Se conserva el módulo `app`** para mantener apariencia y estructura default de Android Studio.
2. **Se conserva `namespace 'org.onebusaway.android'`** porque coincide con el proyecto nuevo y con el código original.
3. **Se conserva el `applicationId` del flavor original `oba`: `com.joulespersecond.seattlebusbot`**, porque el `google-services.json` incluido en el proyecto original solo contiene ese paquete. Cambiarlo a `org.onebusaway.android` haría fallar el plugin Google Services hasta generar un Firebase config nuevo.
4. **Se migraron los plugins al modelo moderno de Version Catalog** en vez de usar `buildscript { classpath ... }`.
5. **Se movieron los repositorios de dependencias a `settings.gradle`** para poder mantener `repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)` del proyecto nuevo.
6. **Se agregó el plugin Kotlin Android** porque el código original contiene fuentes `.kt` en `src/main`, `src/google`, `test` y `androidTest`.

## Variant principal

En Android Studio selecciona:

```text
Build Variants > app > obaGoogleDebug
```

Comando equivalente:

```bash
./gradlew :app:assembleObaGoogleDebug
```

## Archivos clave adaptados

- `settings.gradle`
- `build.gradle`
- `gradle/libs.versions.toml`
- `gradle.properties`
- `app/build.gradle`
- `app/src/**`
- `app/flavors/**`
- `app/schemas/**`

