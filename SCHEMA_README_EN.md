# Korean Modern Literary Criticism TEI XML Schema

A customized TEI P5-based XML schema for digital humanities research on Korean modern literary criticism texts

## Overview

This schema (`tei-criticism-schema.xsd`) is designed based on TEI (Text Encoding Initiative) P5 guidelines while reflecting the unique characteristics of Korean modern literary criticism texts. It enables structured recording of critics' evaluative discourse, citation patterns, and conceptual terminology usage.

## Namespace

```xml
xmlns="http://www.tei-c.org/ns/1.0"
```

## Document Structure

TEI documents follow this hierarchical structure:

```
TEI
├── teiHeader (metadata)
│   ├── fileDesc (bibliographic information)
│   │   ├── titleStmt (title, author, responsibility)
│   │   ├── publicationStmt (publication information)
│   │   └── sourceDesc (source information)
│   └── encodingDesc (encoding policies)
│       ├── editorialDecl (editorial principles)
│       ├── tagsDecl (tag usage declaration)
│       └── classDecl (classification system)
└── text (content)
    ├── front (front matter) - optional
    ├── body (main content) - required
    └── back (back matter) - optional
```

## Enumeration Types

### DivTypeEnum - Division Types

| Value | Description |
|-------|-------------|
| `contents` | Table of contents |
| `introduction` | Introduction |
| `body` | Main body |
| `conclusion` | Conclusion |
| `section` | Section/subsection |
| `argument` | Argument/thesis |
| `criticism` | Literary criticism |
| `review` | Book review |
| `editorial` | Editorial |
| `column` | Column |
| `interview` | Interview |
| `notes` | Notes/remarks |

### TitleLevelEnum - Title Hierarchy

| Value | Description |
|-------|-------------|
| `m` | Monograph - complete book title |
| `a` | Analytic - article/chapter title |
| `j` | Journal - serial publication title |

### TitleTypeEnum - Title Genre

| Value | Description |
|-------|-------------|
| `critic` | Criticism |
| `novel` | Novel |
| `poem` | Poetry |
| `play` | Drama |
| `essay` | Essay |
| `translation` | Translation |
| `children` | Children's literature |
| `contribution` | Contribution |
| `foreign` | Foreign literature |
| `journal` | Academic journal |
| `newspaper` | Newspaper |
| `coterie` | Coterie magazine |
| `publication` | Publication |
| `other` | Other |

### QuoteTypeEnum - Quotation Types

| Value | Description |
|-------|-------------|
| `direct` | Direct quotation |
| `indirect` | Indirect quotation |
| `paraphrase` | Paraphrase/summary |
| `contribution` | Contribution citation |
| `criticism` | Criticism citation |
| `review` | Review citation |
| `commentary` | Commentary citation |

### InterpValueEnum - Evaluation Stance

| Value | Description |
|-------|-------------|
| `affirmative` | Positive evaluation |
| `neutral` | Neutral description |
| `critical` | Critical/negative evaluation |

### RoleEnum - Person Roles

| Value | Description |
|-------|-------------|
| `critic` | Critic |
| `novelist` | Novelist |
| `poet` | Poet |
| `playwright` | Playwright |
| `essayist` | Essayist |
| `translator` | Translator |
| `childrenauthor` | Children's literature author |
| `scholar` | Scholar/researcher |
| `foreigner` | Foreign literary figure |
| `other` | Other |

## Core Element Types

### Personal Name (PersNameType)

```xml
<persName 
  id="p-imhwa" 
  role="critic poet" 
  ref="https://encykorea.aks.ac.kr/Article/E0047762">
  Im Hwa
</persName>
```

| Attribute | Type | Description |
|-----------|------|-------------|
| `id` | ID | Unique identifier |
| `role` | RoleList | Roles (space-separated for multiple) |
| `ref` | string | External reference URI |

### Title (TitleInlineType)

```xml
<title level="a" type="critic" ref="https://...">
  Introduction to New Literature History
</title>
```

| Attribute | Type | Description |
|-----------|------|-------------|
| `level` | TitleLevelEnum | Title hierarchy |
| `type` | TitleTypeEnum | Genre/nature |
| `id` | ID | Unique identifier |
| `ref` | string | External reference |

### Term (TermType)

```xml
<term type="concept" id="t-modernity">
  modernity
</term>
```

| Attribute | Type | Description |
|-----------|------|-------------|
| `type` | string | Term classification (e.g., "concept", "movement") |
| `id` | ID | Unique identifier |
| `ref` | string | External reference |

### Quote (QuoteType)

```xml
<quote type="direct" genre="critic" source="Kim Ki-rim, Poetics">
  "Poetry is the architecture of language."
</quote>
```

| Attribute | Type | Description |
|-----------|------|-------------|
| `type` | QuoteTypeEnum | Quotation method |
| `genre` | QuoteGenreEnum | Genre of quoted source |
| `source` | string | Source reference |
| `ana` | IDREFS | Analysis/annotation link |

### Interpretation/Evaluation (InterpType)

```xml
<interp value="affirmative" ana="Recognition of literary historical significance">
  It can be evaluated as the starting point of modern Korean literature.
</interp>
```

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| `value` | InterpValueEnum | Optional | Evaluation stance |
| `ana` | string | **Required** | Analysis basis/criteria |

### Note (NoteType)

```xml
<note type="footnote" target="fn1">
  Originally written as '文學' in the source text.
</note>
```

| Attribute | Type | Description |
|-----------|------|-------------|
| `type` | string | Note type |
| `target` | string | Link target |
| `ana` | string | Analysis information |

## Document Structure Elements

### Sentence (SentenceType)

```xml
<s id="s1">
  <persName role="critic">Baek Cheol</persName> evaluated 
  <title type="novel">Mujeong</title> as 
  <interp value="affirmative" ana="literary historical evaluation">
    the beginning of modern literature
  </interp>.
</s>
```

Allowed child elements:
- `persName`, `title`, `orgName`, `term`
- `quote`, `interp`, `note`, `ref`
- `lb` (line break)

### Paragraph (ParagraphType)

```xml
<p>
  <s>First sentence.</s>
  <s>Second sentence.</s>
</p>
```

### Division (DivType)

```xml
<div type="introduction" id="div-intro">
  <head>Introduction</head>
  <p>
    <s>The purpose of this study is...</s>
  </p>
</div>
```

## Bibliographic Information

### Structured Bibliography (BiblStructType)

```xml
<biblStruct type="journal">
  <analytic>
    <title>Introduction to New Literature History</title>
    <author><persName>Im Hwa</persName></author>
  </analytic>
  <monogr>
    <title>Chosun Ilbo</title>
    <author><persName>Editorial Department</persName></author>
    <imprint>
      <pubPlace>Seoul</pubPlace>
      <publisher>Chosun Ilbo Press</publisher>
      <date when="1935-10-09">October 9, 1935</date>
    </imprint>
  </monogr>
</biblStruct>
```

### Simple Bibliography (BiblSimpleType)

```xml
<bibl type="publication">
  <title>History of New Korean Literary Trends</title>, Baek Cheol, 1948
</bibl>
```

## Classification System Definition

```xml
<classDecl>
  <taxonomy id="genre">
    <category id="gen-poetry">
      <catDesc>Poetry</catDesc>
    </category>
    <category id="gen-novel">
      <catDesc>Novel</catDesc>
    </category>
  </taxonomy>
  <taxonomy id="evaluation">
    <category id="eval-positive">
      <catDesc>Positive evaluation</catDesc>
    </category>
  </taxonomy>
</classDecl>
```

## Complete Document Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<TEI xmlns="http://www.tei-c.org/ns/1.0">
  <teiHeader>
    <fileDesc>
      <titleStmt>
        <title>History of New Korean Literary Trends (XML Data)</title>
        <author><persName>Baek Cheol</persName></author>
        <respStmt>
          <resp>XML Encoding</resp>
          <name>Lee Byeong-Joo</name>
        </respStmt>
      </titleStmt>
      <publicationStmt>
        <p>Research-use non-public data</p>
      </publicationStmt>
      <sourceDesc>
        <biblStruct type="publication">
          <monogr>
            <title>History of New Korean Literary Trends</title>
            <author><persName>Baek Cheol</persName></author>
            <imprint>
              <pubPlace>Seoul</pubPlace>
              <publisher>Suseonsa</publisher>
              <date when="1948">1948</date>
            </imprint>
          </monogr>
        </biblStruct>
      </sourceDesc>
    </fileDesc>
    <encodingDesc>
      <editorialDecl>
        <p>Preserving the original mixed Korean-Chinese script with modern readings annotated</p>
      </editorialDecl>
      <tagsDecl>
        <namespace>
          <tagUsage gi="persName" occurs="150"/>
          <tagUsage gi="title" occurs="80"/>
          <tagUsage gi="interp" occurs="45"/>
        </namespace>
      </tagsDecl>
      <classDecl>
        <taxonomy id="role">
          <category id="role-critic">
            <catDesc>Critic</catDesc>
          </category>
        </taxonomy>
      </classDecl>
    </encodingDesc>
  </teiHeader>
  
  <text>
    <front>
      <div type="contents">
        <head>Table of Contents</head>
        <list>
          <item n="1">The Dawn of New Literature</item>
          <item n="2">Changga and New Novels</item>
        </list>
      </div>
    </front>
    
    <body>
      <div type="section" id="ch1">
        <head>Chapter 1: The Dawn of New Literature</head>
        <p>
          <s id="s1">
            Before <term type="concept">new literature</term> emerged 
            in the form of <term type="concept">changga</term> or 
            <term type="concept">new novels</term>, 
            <interp value="affirmative" ana="Recognition of translation's pioneering role">
              we can infer that translation activities preceded 
              as a direct preparatory process
            </interp>.
          </s>
        </p>
      </div>
    </body>
    
    <back>
      <div type="notes">
        <head>Notes</head>
        <p>
          <s>Original footnotes and editorial annotations</s>
        </p>
      </div>
    </back>
  </text>
</TEI>
```

## Validation

To verify that your XML document conforms to this schema:

```bash
# Using xmllint
xmllint --schema tei-criticism-schema.xsd your-document.xml --noout

# Using Python lxml
from lxml import etree
schema = etree.XMLSchema(etree.parse('tei-criticism-schema.xsd'))
schema.validate(etree.parse('your-document.xml'))
```

## Important Notes

1. **body is required**: `<body>` must be included within `<text>`.
2. **Order matters**: Must follow `front` → `body` → `back` sequence.
3. **ana is required for interp**: The `ana` attribute of `<interp>` is mandatory.
4. **Namespace declaration**: The TEI namespace must be declared.

## External Data Connections

The `ref` attribute can link to the following external databases:

- [ISNI](https://isni.org/) - International Standard Name Identifier
- [Wikidata](https://www.wikidata.org/)
- [Encyclopedia of Korean Culture](https://encykorea.aks.ac.kr/)
- [Database of Korean History](https://db.history.go.kr/)

## References

- [TEI P5 Guidelines](https://tei-c.org/release/doc/tei-p5-doc/en/html/index.html)
- [Kim Baro et al., *XML(TEI) with Humanities*](https://wikidocs.net/book/14569)

## License

This schema is freely available for academic research purposes.

## Author

Lee, Byeong-Joo (Department of Language and Literature, Korea Air Force Academy)

---

*This schema was developed with support from the National Research Foundation of Korea (NRF-2023S1A5A8079304).*
