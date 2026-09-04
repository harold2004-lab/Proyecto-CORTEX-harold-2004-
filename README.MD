# Proyecto CORTEX - Sistema Gatekeeper

## 🎯 Objetivo General
Crear un sistema inteligente de filtrado de información que identifique y procese mensajes relevantes mientras elimina ruido, priorizando atención en información clave.

---

## 📋 Definición de "Ruido"

### ¿Qué es Ruido en CORTEX?
El **ruido** es cualquier información que:
- ✗ No contribuye al objetivo principal de la conversación
- ✗ Contiene información redundante o repetida
- ✗ Incluye palabras vacías sin valor semántico
- ✗ Son detalles innecesarios o contexto irrelevante
- ✗ Generan distracción del propósito central

---

## 🚪 Reglas de Atención - Gatekeeper (GitHub)

### Regla 1: Filtro de Longitud
```
SI mensaje.palabras > 500 ENTONCES:
  - Activar modo "Compresión de Atención"
  - Extraer SOLO: sustantivos clave + última oración
  - Descartar: adjetivos secundarios, ejemplos, explicaciones extensas
```

### Regla 2: Identificación de Sustantivos Clave
```
SUSTANTIVOS CLAVE = palabras que:
  ✓ Son entidades principales (objetos, personas, conceptos)
  ✓ Se repiten 2+ veces en el mensaje
  ✓ Aparecen en posición inicial de oraciones
  ✓ Son sujetos o complementos diretos de verbos críticos
```

### Regla 3: Prioridad de la Última Frase
```
ÚLTIMA FRASE = información de mayor prioridad porque:
  ✓ Contiene frecuentemente la conclusión o llamada a acción
  ✓ Representa la intención final del emisor
  ✓ Sintetiza el pensamiento completo
  ✓ Tiene máximo peso en toma de decisiones
```

### Regla 4: Eliminación de Ruido Común
```
ELIMINAR AUTOMÁTICAMENTE:
  • Palabras vacías: "el", "la", "un", "una", "por", "para"
  • Rellenos: "bueno", "así que", "obviamente", "básicamente"
  • Fórmulas de cortesía: "por favor", "gracias", "disculpa"
  • Redundancias: texto que repite información ya mencionada
  • Conectores débiles: "entonces", "además", "también" (en exceso)
```

### Regla 5: Análisis de Densidad Informativa
```
DENSIDAD = Palabras Clave / Palabras Totales

SI densidad < 15% ENTONCES: Mensaje Alto en Ruido (priorizar compresión)
SI densidad 15-30% ENTONCES: Mensaje Normal (filtrado estándar)
SI densidad > 30% ENTONCES: Mensaje Alto en Valor (procesar completo)
```

### Regla 6: Contexto y Relevancia
```
EVALUAR RELEVANCIA por:
  ✓ Conexión con objetivo del proyecto
  ✓ Conexión con conversación anterior
  ✓ Necesidad para toma de decisiones
  ✓ Impacto en acciones siguientes
  
SI no cumple criterios → CLASIFICAR COMO RUIDO
```

### Regla 7: Prioridad Jerárquica
```
NIVEL 1 (Máxima Prioridad):
  • Sustantivos clave + última frase
  • Llamadas a acción explícitas

NIVEL 2 (Prioridad Media):
  • Verbos de acción asociados a sustantivos clave
  • Datos numéricos específicos

NIVEL 3 (Prioridad Baja):
  • Ejemplos ilustrativos
  • Contexto histórico
  • Información de apoyo

DESCARTAR:
  • Especulaciones sin base
  • Comentarios tangenciales
  • Opiniones no estructuradas
```

---

## 🔧 Algoritmo de Procesamiento

```
INPUT: Mensaje de cualquier longitud
│
├─ PASO 1: Contar palabras
│  └─ Si > 500 palabras → Activar Compresión
│
├─ PASO 2: Extraer sustantivos clave
│  ├─ Análisis POS (Part of Speech)
│  ├─ Identificar frecuencia
│  └─ Filtrar por relevancia contextual
│
├─ PASO 3: Capturar última oración
│  └─ Validar que contiene información crítica
│
├─ PASO 4: Calcular densidad informativa
│  └─ Determinar nivel de compresión necesario
│
├─ PASO 5: Eliminar ruido identificado
│  ├─ Palabras vacías
│  ├─ Redundancias
│  └─ Conectores débiles
│
└─ OUTPUT: Mensaje comprimido con máxima información relevante
```

---

## 📊 Ejemplo Práctico

### Input (567 palabras - LARGO):
```
"He estado pensando en el proyecto y bueno, creo que deberíamos 
realmente considerar la implementación de un sistema de autenticación 
robusto, y además, también sería importante pensar en cómo manejamos 
la seguridad de los datos del usuario, porque básicamente, los datos 
son críticos para la operación del sistema. Además, también deberíamos 
considerar... [más texto redundante]... En conclusión, necesitamos 
implementar OAuth2 con cifrado de extremo a extremo."
```

### Processing (Gatekeeper):
1. ✓ Detecta > 500 palabras → ACTIVAR COMPRESIÓN
2. ✓ Extrae sustantivos clave: **[sistema, autenticación, seguridad, datos, usuario, OAuth2, cifrado]**
3. ✓ Identifica última frase: **"necesitamos implementar OAuth2 con cifrado de extremo a extremo"**
4. ✓ Elimina ruido: "bueno", "básicamente", "además", "también" (repetido)

### Output (COMPRIMIDO):
```
SUSTANTIVOS CLAVE: sistema, autenticación, seguridad, datos, usuario, OAuth2, cifrado
ACCIÓN FINAL: Implementar OAuth2 con cifrado de extremo a extremo
```

---

## ✅ Criterios de Validación

- [ ] ¿Se preservó toda información crítica?
- [ ] ¿La compresión es > 40%?
- [ ] ¿La última frase está intacta?
- [ ] ¿Los sustantivos clave son identificables?
- [ ] ¿Se eliminó ruido sin perder contexto?

---

## 🔄 Próximos Pasos

1. Implementar análisis de POS (Part-of-Speech)
2. Crear base de datos de palabras vacías en español
3. Desarrollar clasificador de relevancia
4. Integrar con sistema de atención de IA
5. Validar con pruebas en conversaciones reales

---

**Versión:** 1.0  
**Última actualización:** 2026-09-04  
**Proyecto:** CORTEX - Gatekeeper System
