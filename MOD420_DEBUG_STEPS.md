# Solución del Error MOD420

## Cambios Realizados

### 1. **Flags de Java para JAXB y Apache CXF** ✅

Se agregaron los siguientes flags al comando Java:

```
--add-opens java.base/java.lang=ALL-UNNAMED
--add-opens java.base/java.lang.reflect=ALL-UNNAMED
--add-opens java.base/java.io=ALL-UNNAMED
--add-opens java.base/java.net=ALL-UNNAMED
--add-opens java.base/java.util=ALL-UNNAMED
--add-opens java.base/java.util.concurrent=ALL-UNNAMED
```

Esto soluciona los errores `InaccessibleObjectException` que ocurrían al intentar
ejecutar el JAR.

### 2. **Mejora de Manejo de Errores** ✅

Se mejoró el método `_atc_run_cmd()` para:

- Capturar errores adicionales del archivo `FICH_ERRORES.txt`
- Mostrar los primeros 500 caracteres del XML generado para depuración
- Diferenciar entre excepciones de usuario y otras excepciones

**Archivo:**
`/home/binhex/Documentos/Practica-Odoo-17/odoo/custom/src/l10n-spain/l10n_es_atc/models/l10n_es_atc_report.py`

### 3. **Limpieza de Atributos None en XML** ✅

Se creó un método helper `_atc_clean_attr()` para evitar que se generen atributos XML
con valor `None`.

Se actualizar el template del MOD420 para usar este método:

**Archivo:**
`/home/binhex/Documentos/Practica-Odoo-17/odoo/custom/src/l10n-spain/l10n_es_atc_mod420/reports/mod420_report.xml`

## Próximos Pasos

1. **Reinicia Odoo:**

   ```bash
   cd /home/binhex/Documentos/Practica-Odoo-17
   # O usa el botón "Restart Odoo" en VS Code
   ```

2. **Prueba nuevamente generar el MOD420**

3. **Si aún hay errores**, el mensaje de error ahora incluirá:
   - El archivo `FICH_ERRORES.txt` completo si existe
   - Los primeros 500 caracteres del XML generado
   - Lo que te permitirá identificar qué está mal

## Posibles Causas de "Declaración no generada"

Si recibes este error, generalmente significa que:

1. **Datos incompletos o inválidos** - Verifica que:

   - La empresa tenga NIF válido
   - La dirección de la empresa esté completa
   - El código postal esté presente
   - La provincia esté configurada correctamente

2. **Campos de MOD420 no rellenados** - Asegúrate de:

   - Que el `statement_type` sea válido ('N' para normal, 'C' para complementaria)
   - Que los importes sean coherentes

3. **XML malformado** - El XML mostrado en el error te indicará qué nodo es inválido

## Archivo de Log

Si necesitas depuración adicional, los ficheros XML se generan en:

```
/tmp/modelo420/modelo420.xml
```

Puedes revisar este fichero para validar su estructura.

---

**Último actualizado:** 14 de noviembre de 2025
