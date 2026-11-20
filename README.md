# AR-LEKO — Ontología de Conocimiento Jurídico Argentino

**Nombre en inglés:** Argentine Legal Knowledge Ontology  
**Versión:** 1.3.0  
**Serialización:** RDF 1.1 Turtle (`.ttl`)  
**Lenguaje ontológico:** OWL 2  
**Idioma principal:** castellano (`es`)  
**Idiomas adicionales:** inglés (`en`) y portugués (`pt`)

**IRI de la ontología:** `https://w3id.org/arleko`  
**Namespace de entidades:** `https://w3id.org/arleko#`  
**Namespace de vocabularios controlados:** `https://w3id.org/arleko/vocab#`  
**Licencia:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)  
**Repositorio:** [github.com/ar-leko/ar-leko-ontology](https://github.com/ar-leko/ar-leko-ontology)

> **Estado del identificador persistente:** el código está en [ar-leko/ar-leko-ontology](https://github.com/ar-leko/ar-leko-ontology). El namespace `w3id.org/arleko` está libre y las reglas de redirección están en `publication/w3id/ids/arleko/`. No resuelve hasta que el pull request a [perma-id/w3id.org](https://github.com/perma-id/w3id.org) se fusione. La documentación HTML se publica en `https://ar-leko.github.io/ar-leko-ontology/`.

---

## 1. Qué es AR-LEKO

AR-LEKO es una ontología OWL 2 para representar normas jurídicas argentinas de distintos niveles y organismos emisores mediante datos enlazados (RDF). Su objetivo es proporcionar un modelo común para describir la identidad de una norma, su estructura interna, sus versiones temporales, sus modificaciones, sus referencias cruzadas y el contexto institucional y territorial en el que se dicta y aplica.

La ontología está pensada para construir grafos de conocimiento jurídicos, integrar fuentes normativas, facilitar búsquedas estructuradas y mantener trazabilidad entre normas y sus cambios a lo largo del tiempo.

AR-LEKO es un modelo conceptual. No contiene por sí misma un corpus oficial de legislación, no certifica que una norma esté vigente y no sustituye la interpretación jurídica. La calidad de los datos depende de las fuentes utilizadas, los procesos de extracción y la curación de los registros.

## 2. Modelo conceptual

### 2.1. Clases principales

| Clase | Qué representa |
| :--- | :--- |
| `arleko:ObraJuridica` | Obra jurídica estable que puede tener versiones, ser modificada, derogada o citada. |
| `arleko:Norma` | Instrumento jurídico: constitución, tratado, ley, código, decreto, resolución, circular u ordenanza, entre otros. |
| `arleko:UnidadNormativa` | División estructural de una norma: libro, título, capítulo, artículo, inciso, apartado o anexo. |
| `arleko:Version` | Expresión textual o temporal de una obra jurídica. |
| `arleko:VersionConsolidada` | Versión consolidada de una obra jurídica. |
| `arleko:ActoModificatorio` | Acto que modifica, deroga, suspende, corrige o produce otro efecto sobre una obra jurídica. |
| `arleko:Referencia` | Referencia de una obra o versión jurídica a otra obra jurídica. |
| `arleko:EdicionBoletinOficial` | Edición de un boletín oficial en la que puede publicarse una norma. |
| `arleko:OrganoEmisor` | Institución o autoridad que interviene en la emisión, sanción o promulgación de una norma. |
| `arleko:Jurisdiccion` | Orden jurídico o ámbito jurisdiccional, por ejemplo nacional, provincial, CABA o municipal. |
| `arleko:SujetoRegulado` | Persona o entidad destinataria de una norma. |
| `arleko:UnidadTerritorial` | Unidad geográfica o administrativa del territorio. |

`arleko:Jurisdiccion` y `arleko:UnidadTerritorial` no se declaran clases disjuntas. Una provincia, por ejemplo, puede representarse como unidad territorial y también servir de referente a una jurisdicción. Ambas clases describen dimensiones diferentes de una misma entidad.

### 2.2. Propiedades principales

**Estructura normativa**
- `esParteDe` / `tieneParte`
- `esHijoDe` / `tieneHijo`
- `perteneceANorma` / `tieneUnidad`

**Versionado**
- `esVersionDe` / `tieneVersion`
- `versionAnterior` / `versionSiguiente`
- `tipoVersion`
- `fechaDesde` / `fechaHasta`

**Modificaciones y efectos jurídicos**
- `obraActuante` / `realizaActo`
- `obraDestino` / `afectadaPorActo`
- `produceVersion` / `creadaPorActo`
- `cierraVersion` / `cerradaPorActo`
- `modifica`, `enmienda`, `deroga`, `reemplaza`, `suspende`, `corrige` y `reglamenta`

**Referencias**
- `fuenteReferencia`
- `destinoReferencia`
- `versionFuenteReferencia`
- `versionDestinoReferencia`
- `tipoReferencia`
- `modoReferencia`

**Clasificación, jurisdicción y territorio**
- `tipoNorma`, `tipoNivel`, `materia`
- `jurisdiccion`, `jurisdiccionPadre`, `nivelJurisdiccion`
- `tipoUnidadTerritorial`, `unidadTerritorialPadre`, `ambitoTerritorial`
- `sujetoDestinatario`, `tipoSujeto`

**Órganos y publicación**
- `emitidaPor`, `sancionadaPor`, `promulgadaPor`
- `publicadaEn`, `modoPromulgacion`
- `tipoOrgano`, `organismoPadre`, `predecesorOrgano`, `sucesorOrgano`

Las propiedades `sancionadaPor`, `promulgadaPor` y `emitidaPor` representan intervenciones jurídicas diferentes y no deben utilizarse como equivalentes.

### 2.3. Propiedades de datos

Entre las propiedades de datos principales se encuentran:

- **Identificación:** `identificadorLocal`, `identificadorExterno`, `idInfoLEG`, `idSAIJ`, `numeroNorma`, `anioNorma`, `designacionOficial`.
- **Títulos y descripciones:** `titulo`, `tituloCorto`, `nombrePopular`, `descripcion`, `resumenEjecutivo`.
- **Fechas normativas:** `fechaNorma`, `fechaSancion`, `fechaPromulgada`, `fechaDictada`, `fechaPublicacion`, `fechaEntradaVigencia`, `fechaCeseVigencia`, `fechaVeto`, `fechaFirmaTratado`, `fechaRatificacion`.
- **Contenido y temporalidad de versiones:** `fechaDesde`, `fechaHasta`, `texto`, `epigrafe`, `etiquetaNumero`, `numeroBase`, `sufijoNumero`, `posicion`, `documentoFuente`, `esTextoOrdenado`.
- **Evidencia de modificaciones y referencias:** `vigenteDesde`, `textoEvidencia`, `textoAncla`, `estaResuelta`, `textoDestinoNoResuelto`, `confianzaExtraccion`.
- **Boletines y órganos:** `nombreBoletin`, `numeroEdicion`, `fechaEdicion`, `denominacionAnterior`, `fechaInicioActividad`, `fechaCeseActividad`, `codigoOrgano`.

La lista anterior resume propiedades representativas; no constituye un inventario exhaustivo de todas las propiedades definidas en el archivo Turtle.

## 3. Sanción, promulgación y emisión de normas

En el procedimiento de formación de las leyes argentinas conviene distinguir tres momentos y responsabilidades:

1. **Sanción:** el órgano legislativo aprueba el proyecto de ley.
2. **Promulgación:** el Poder Ejecutivo promulga la ley, de forma expresa o tácita, según corresponda.
3. **Publicación:** la norma se publica en el boletín oficial correspondiente.

Por ello, AR-LEKO distingue:

| Propiedad | Uso |
| :--- | :--- |
| `arleko:sancionadaPor` | Órgano legislativo que sanciona una ley. |
| `arleko:promulgadaPor` | Poder Ejecutivo que promulga una ley. |
| `arleko:emitidaPor` | Autoridad que dicta directamente un acto, por ejemplo una resolución administrativa. |

El Congreso Nacional, las legislaturas provinciales y los concejos deliberantes pueden modelarse como `arleko:OrganoEmisor` por su rol institucional dentro del modelo. Sin embargo, para una ley debe utilizarse `sancionadaPor` para identificar al órgano legislativo, y no `emitidaPor`.

## 4. Jurisdicciones y unidades territoriales

AR-LEKO diferencia el orden jurídico (`Jurisdiccion`) de la unidad territorial (`UnidadTerritorial`). La relación `unidadTerritorialPadre` permite representar jerarquías territoriales, por ejemplo municipio → departamento o partido → provincia → Nación, cuando esa estructura corresponda a la jurisdicción concreta.

El modelo contempla conceptos territoriales como Nación, provincia, Ciudad Autónoma de Buenos Aires, municipio, departamento, partido y comuna. La estructura administrativa no es uniforme en todo el país: debe completarse con fuentes oficiales específicas de cada jurisdicción y no asumirse una jerarquía única e invariable.

### 4.1. Ámbitos marítimos

El esquema `EsquemaAmbitoMaritimo` permite describir espacios marítimos relevantes para el ámbito territorial de una norma, entre ellos:

- `AmbitoMaritimo-MarTerritorial`
- `AmbitoMaritimo-ZonaContigua`
- `AmbitoMaritimo-ZonaEconomicaExclusiva`
- `AmbitoMaritimo-PlataformaContinental`
- `AmbitoMaritimo-AltaMar`

La inclusión de `AltaMar` es descriptiva: identifica un contexto geográfico y no implica soberanía ni jurisdicción argentina sobre alta mar. El régimen jurídico aplicable debe representarse e interpretarse por separado.

## 5. Estados de una norma: tres dimensiones independientes

### 5.1. Cambio de modelado en la versión 1.3.0

La versión 1.3.0 separa tres dimensiones que antes estaban agrupadas en un único estado legal. Esta modificación evita tratar como mutuamente excluyentes situaciones que pueden coexistir. Por ejemplo, una norma puede estar vigente, haber sido modificada y tener su aplicación suspendida en un período determinado.

| Dimensión | Propiedad | Qué describe |
| :--- | :--- | :--- |
| Vigencia | `estadoVigenciaActual` | Si la norma está vigente, derogada, anulada, caduca o pendiente de entrada en vigor, entre otros estados de vigencia. |
| Aplicación | `estadoAplicacionActual` | Si la aplicación de la norma es aplicable o está suspendida. |
| Modificación | `estadoModificacionActual` | Si la norma ha sido modificada o no, como dimensión de su historial de cambios. |

`estadoLegalActual` se conserva en la versión 1.3.0 como propiedad obsoleta (`deprecated`) para facilitar compatibilidad con datos anteriores. Los nuevos conjuntos de datos deben utilizar las tres propiedades específicas.

### 5.2. Esquemas de conceptos

Los estados se organizan en esquemas SKOS separados:

- `EsquemaEstadoLegal`: estados relacionados con la vigencia.
- `EsquemaEstadoAplicacion`: estados relacionados con la aplicabilidad.
- `EsquemaEstadoModificacion`: estados relacionados con el historial de modificaciones.

En particular, `EstadoModificacion-Modificada` pertenece a `EsquemaEstadoModificacion`, no al esquema de vigencia. Del mismo modo, `EstadoAplicacion-Suspendida` pertenece al esquema de aplicabilidad. Una suspensión de aplicación no significa necesariamente que la norma haya dejado de estar formalmente vigente.

La clasificación de una norma debe basarse en evidencia jurídica y documental. La ontología permite registrar los estados y sus relaciones, pero no determina automáticamente sus consecuencias jurídicas.

## 6. Vocabularios controlados

La ontología utiliza SKOS para organizar clasificaciones y listas de conceptos controlados. La versión 1.3.0 incluye esquemas para:

- Tipos de normas (`EsquemaTipoNorma`).
- Niveles de unidades normativas (`EsquemaNivelUnidad`).
- Tipos de modificación (`EsquemaTipoModificacion`).
- Tipos y modos de referencia (`EsquemaTipoReferencia`, `EsquemaModoReferencia`).
- Vigencia, aplicación y modificación (`EsquemaEstadoLegal`, `EsquemaEstadoAplicacion`, `EsquemaEstadoModificacion`).
- Tipos de versión (`EsquemaTipoVersion`).
- Niveles de jurisdicción (`EsquemaNivelJurisdiccion`).
- Unidades territoriales (`EsquemaUnidadTerritorial`).
- Ámbitos marítimos (`EsquemaAmbitoMaritimo`).
- Tipos de órgano (`EsquemaTipoOrgano`).
- Modos de promulgación (`EsquemaModoPromulgacion`).

## 7. Alineación con estándares externos

AR-LEKO reutiliza vocabularios externos y puede convivir con los sistemas de información jurídica latinoamericanos.

- **SKOS:** `skos:Concept`, `skos:ConceptScheme`, `skos:inScheme`, `skos:prefLabel`, `skos:definition`, `skos:broader` y otros términos relacionados.
- **ELI (European Legislation Identifier):** determinadas clases y propiedades, entre ellas `eli:LegalResource`, `eli:LegalExpression`, `eli:LegalResourceSubdivision`, `eli:amends`, `eli:repeals`, `eli:cites`, `eli:based_on`, `eli:corrects`, `eli:has_part` y `eli:is_part_of`.
- **Sistemas latinoamericanos:** `idInfoLEG` e `idSAIJ` conservan los identificadores de InfoLEG y del SAIJ. `identificadorExterno` guarda el identificador de otro catálogo oficial de la región, como LexML en Brasil o el sistema de información legislativa de otro país. Las etiquetas en castellano y en portugués, y los tipos de norma del derecho continental —ley, decreto, código, resolución, ordenanza, tratado—, permiten describir instrumentos equivalentes de otros ordenamientos latinoamericanos junto con las normas argentinas.

La versión actual referencia los IRI canónicos de SKOS y de ELI, y utiliza alineaciones seleccionadas mediante `rdfs:subClassOf` y `rdfs:subPropertyOf`. No declara `owl:imports` de las ontologías completas de SKOS o ELI, ni de los sistemas latinoamericanos. Las aplicaciones que necesiten todos los axiomas externos deberán cargar esos vocabularios por separado.

Esta reutilización no implica certificación formal por ELI, por InfoLEG, por el SAIJ ni por los demás sistemas de la región, ni equivalencia completa entre AR-LEKO y esos vocabularios.

## 8. Identificadores y versionado

Los identificadores de la versión 1.3.0 son:

- IRI de la ontología: `https://w3id.org/arleko`
- IRI de versión: `https://w3id.org/arleko/1.3.0`
- Namespace de entidades AR-LEKO: `https://w3id.org/arleko#`
- Namespace de vocabularios AR-LEKO: `https://w3id.org/arleko/vocab#`

El IRI de la ontología debe mantenerse estable entre versiones. El IRI de versión debe cambiar con cada release. El repositorio [github.com/ar-leko/ar-leko-ontology](https://github.com/ar-leko/ar-leko-ontology) identifica la ubicación del código y los artefactos publicados, no la identidad conceptual de la ontología.

La negociación de contenido responde `303 See Other`: Turtle, JSON-LD, RDF/XML y N-Triples salen de jsDelivr con su tipo de medio registrado; el navegador recibe la documentación HTML de GitHub Pages. `https://w3id.org/arleko/vocab` sirve el mismo documento, porque los conceptos controlados están definidos ahí. Hasta que el pull request se fusione, estos IRI se usan en los datos pero no deben anunciarse como identificadores que ya resuelven.

## 9. Ejemplo de datos

El siguiente ejemplo es ilustrativo. No representa una norma real ni afirma cuál es su estado jurídico actual.

```turtle
@prefix arleko: <https://w3id.org/arleko#> .
@prefix arlekov: <https://w3id.org/arleko/vocab#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://data.example.org/norm/example-law>
    a arleko:Norma ;
    arleko:tipoNorma arlekov:TipoNorma-Ley ;
    arleko:numeroNorma "12345" ;
    arleko:anioNorma "2020"^^xsd:gYear ;
    arleko:estadoVigenciaActual arlekov:EstadoLegal-Vigente ;
    arleko:estadoAplicacionActual arlekov:EstadoAplicacion-Aplicable ;
    arleko:estadoModificacionActual arlekov:EstadoModificacion-Modificada .
```

En conjuntos de datos de producción, los IRI de las instancias deben seguir una política estable de identificación. Siempre que sea posible, deben conservarse los identificadores oficiales, las URL de las fuentes y los datos de procedencia.

## 10. Límites del modelo y trabajo futuro

- AR-LEKO modela normas jurídicas; no es todavía una ontología completa de instituciones judiciales, causas, expedientes, pruebas, sentencias o procedimientos.
- Los valores de `rangoJerarquico` asociados a tipos de normas son una ayuda de clasificación, no una regla universal para resolver conflictos normativos.
- Las jerarquías territoriales pueden variar entre provincias.
- Los efectos jurídicos de la derogación, suspensión, nulidad y las disposiciones transitorias dependen del derecho aplicable y del contenido del acto correspondiente. La ontología registra clasificaciones y relaciones; no decide automáticamente esos efectos.
- Conviene desarrollar perfiles SHACL diferenciados por fuente de ingestión o producto de datos, porque no todos los campos son obligatorios para todos los tipos de instrumentos jurídicos.
---

## English summary

**AR-LEKO (Argentine Legal Knowledge Ontology), version 1.3.0**, is an OWL 2 ontology serialized in RDF 1.1 Turtle. It provides a model for Argentine legal resources, including legal works, norms, structural units, temporal versions, amending acts, cross-references, institutions, jurisdictions, territorial units and official-gazette publications. Spanish is the primary language, with English and Portuguese labels for interoperability.

The main modeling improvement in version 1.3.0 is the separation of legal status into three independent dimensions: **validity** (`estadoVigenciaActual`), **applicability** (`estadoAplicacionActual`) and **amendment history** (`estadoModificacionActual`). The former `estadoLegalActual` property remains only as deprecated compatibility support. The release also clarifies the distinction between jurisdiction and territory, the treatment of the high seas, and selected alignments with SKOS and ELI. Latin American legal-information systems are linked by identifier: InfoLEG and SAIJ have dedicated properties, and `identificadorExterno` carries the identifier of another official catalog in the region.
