# 한국 현대문학비평 TEI XML 스키마

한국 현대문학비평 텍스트의 디지털 인문학 연구를 위한 TEI P5 기반 맞춤형 XML 스키마

## 개요

이 스키마(`tei-criticism-schema.xsd`)는 TEI(Text Encoding Initiative) P5 가이드라인을 준용하면서, 한국 현대문학비평 텍스트의 특수성을 반영하여 설계되었습니다. 비평가의 평가적 언술, 인용 양상, 개념어 사용 등을 구조화된 데이터로 기록할 수 있습니다.

## 네임스페이스

```xml
xmlns="http://www.tei-c.org/ns/1.0"
```

## 문서 구조

TEI 문서는 다음과 같은 계층 구조를 따릅니다:

```
TEI
├── teiHeader (메타데이터)
│   ├── fileDesc (서지 정보)
│   │   ├── titleStmt (제목, 저자, 책임표시)
│   │   ├── publicationStmt (출판 정보)
│   │   └── sourceDesc (출처 정보)
│   └── encodingDesc (인코딩 방침)
│       ├── editorialDecl (편집 원칙)
│       ├── tagsDecl (태그 사용 내역)
│       └── classDecl (분류체계)
└── text (본문)
    ├── front (서두) - 선택
    ├── body (본문) - 필수
    └── back (후미) - 선택
```

## 열거형(Enum) 타입

### DivTypeEnum - 구획 유형

| 값 | 설명 |
|---|------|
| `contents` | 목차 |
| `introduction` | 서론 |
| `body` | 본문 |
| `conclusion` | 결론 |
| `section` | 절/섹션 |
| `argument` | 논증 |
| `criticism` | 비평 |
| `review` | 서평/논평 |
| `editorial` | 사설 |
| `column` | 칼럼 |
| `interview` | 인터뷰 |
| `notes` | 주석/비고 |

### TitleLevelEnum - 제목 계층

| 값 | 설명 |
|---|------|
| `m` | 단행본(monograph) - 책 전체 제목 |
| `a` | 분석단위(analytic) - 수록 글 제목 |
| `j` | 저널(journal) - 연속간행물 제목 |

### TitleTypeEnum - 제목 장르

| 값 | 설명 |
|---|------|
| `critic` | 비평문 |
| `novel` | 소설 |
| `poem` | 시 |
| `play` | 희곡 |
| `essay` | 수필 |
| `translation` | 번역 |
| `children` | 아동문학 |
| `contribution` | 기고문 |
| `foreign` | 외국문학 |
| `journal` | 학술지 |
| `newspaper` | 신문 |
| `coterie` | 동인지 |
| `publication` | 출판물 |
| `other` | 기타 |

### QuoteTypeEnum - 인용 유형

| 값 | 설명 |
|---|------|
| `direct` | 직접 인용 |
| `indirect` | 간접 인용 |
| `paraphrase` | 요약/의역 |
| `contribution` | 기고문 인용 |
| `criticism` | 비평문 인용 |
| `review` | 서평 인용 |
| `commentary` | 해설/주석 인용 |

### InterpValueEnum - 평가 태도

| 값 | 설명 |
|---|------|
| `affirmative` | 긍정적 평가 |
| `neutral` | 중립적 서술 |
| `critical` | 비판적/부정적 평가 |

### RoleEnum - 인물 역할

| 값 | 설명 |
|---|------|
| `critic` | 비평가 |
| `novelist` | 소설가 |
| `poet` | 시인 |
| `playwright` | 극작가 |
| `essayist` | 수필가 |
| `translator` | 번역가 |
| `childrenauthor` | 아동문학 작가 |
| `scholar` | 학자/연구자 |
| `foreigner` | 외국 문인 |
| `other` | 기타 |

## 핵심 요소 타입

### 인명 (PersNameType)

```xml
<persName 
  id="p-imhwa" 
  role="critic poet" 
  ref="https://encykorea.aks.ac.kr/Article/E0047762">
  임화
</persName>
```

| 속성 | 타입 | 설명 |
|-----|-----|------|
| `id` | ID | 고유 식별자 |
| `role` | RoleList | 역할 (공백으로 구분하여 복수 지정 가능) |
| `ref` | string | 외부 참조 URI |

### 제목 (TitleInlineType)

```xml
<title level="a" type="critic" ref="https://...">
  신문학사 서론
</title>
```

| 속성 | 타입 | 설명 |
|-----|-----|------|
| `level` | TitleLevelEnum | 제목 계층 |
| `type` | TitleTypeEnum | 장르/성격 |
| `id` | ID | 고유 식별자 |
| `ref` | string | 외부 참조 |

### 용어 (TermType)

```xml
<term type="concept" id="t-modernity">
  근대성
</term>
```

| 속성 | 타입 | 설명 |
|-----|-----|------|
| `type` | string | 용어 분류 (예: "concept", "movement") |
| `id` | ID | 고유 식별자 |
| `ref` | string | 외부 참조 |

### 인용 (QuoteType)

```xml
<quote type="direct" genre="critic" source="김기림, 시론">
  "시는 언어의 건축이다."
</quote>
```

| 속성 | 타입 | 설명 |
|-----|-----|------|
| `type` | QuoteTypeEnum | 인용 방식 |
| `genre` | QuoteGenreEnum | 인용 대상 장르 |
| `source` | string | 출처 |
| `ana` | IDREFS | 분석/주석 연결 |

### 해석/평가 (InterpType)

```xml
<interp value="affirmative" ana="문학사적 의의 인정">
  조선 신문학의 출발점으로 평가할 수 있다.
</interp>
```

| 속성 | 타입 | 필수 | 설명 |
|-----|-----|-----|------|
| `value` | InterpValueEnum | 선택 | 평가 태도 |
| `ana` | string | **필수** | 분석 근거/기준 |

### 주석 (NoteType)

```xml
<note type="footnote" target="fn1">
  원문에는 '文學'으로 표기되어 있음.
</note>
```

| 속성 | 타입 | 설명 |
|-----|-----|------|
| `type` | string | 주석 종류 |
| `target` | string | 연결 대상 |
| `ana` | string | 분석 정보 |

## 문서 구조 요소

### 문장 (SentenceType)

```xml
<s id="s1">
  <persName role="critic">백철</persName>은 
  <title type="novel">무정</title>을 
  <interp value="affirmative" ana="문학사적 평가">
    근대문학의 효시
  </interp>로 평가하였다.
</s>
```

포함 가능한 하위 요소:
- `persName`, `title`, `orgName`, `term`
- `quote`, `interp`, `note`, `ref`
- `lb` (줄바꿈)

### 단락 (ParagraphType)

```xml
<p>
  <s>첫 번째 문장.</s>
  <s>두 번째 문장.</s>
</p>
```

### 구획 (DivType)

```xml
<div type="introduction" id="div-intro">
  <head>서론</head>
  <p>
    <s>본 연구의 목적은...</s>
  </p>
</div>
```

## 서지 정보

### 구조화된 서지 (BiblStructType)

```xml
<biblStruct type="journal">
  <analytic>
    <title>신문학사 서론</title>
    <author><persName>임화</persName></author>
  </analytic>
  <monogr>
    <title>조선일보</title>
    <author><persName>편집부</persName></author>
    <imprint>
      <pubPlace>서울</pubPlace>
      <publisher>조선일보사</publisher>
      <date when="1935-10-09">1935년 10월 9일</date>
    </imprint>
  </monogr>
</biblStruct>
```

### 단순 서지 (BiblSimpleType)

```xml
<bibl type="publication">
  <title>조선신문학사조사</title>, 백철, 1948
</bibl>
```

## 분류체계 정의

```xml
<classDecl>
  <taxonomy id="genre">
    <category id="gen-poetry">
      <catDesc>시</catDesc>
    </category>
    <category id="gen-novel">
      <catDesc>소설</catDesc>
    </category>
  </taxonomy>
  <taxonomy id="evaluation">
    <category id="eval-positive">
      <catDesc>긍정적 평가</catDesc>
    </category>
  </taxonomy>
</classDecl>
```

## 전체 문서 예시

```xml
<?xml version="1.0" encoding="UTF-8"?>
<TEI xmlns="http://www.tei-c.org/ns/1.0">
  <teiHeader>
    <fileDesc>
      <titleStmt>
        <title>조선신문학사조사 (XML 데이터)</title>
        <author><persName>백철</persName></author>
        <respStmt>
          <resp>XML 인코딩</resp>
          <name>이병주</name>
        </respStmt>
      </titleStmt>
      <publicationStmt>
        <p>연구용 비공개 데이터</p>
      </publicationStmt>
      <sourceDesc>
        <biblStruct type="publication">
          <monogr>
            <title>조선신문학사조사</title>
            <author><persName>백철</persName></author>
            <imprint>
              <pubPlace>서울</pubPlace>
              <publisher>수선사</publisher>
              <date when="1948">1948</date>
            </imprint>
          </monogr>
        </biblStruct>
      </sourceDesc>
    </fileDesc>
    <encodingDesc>
      <editorialDecl>
        <p>원문의 국한문혼용체를 유지하고, 현대어 독음을 병기함</p>
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
            <catDesc>비평가</catDesc>
          </category>
        </taxonomy>
      </classDecl>
    </encodingDesc>
  </teiHeader>
  
  <text>
    <front>
      <div type="contents">
        <head>목차</head>
        <list>
          <item n="1">신문학 태동기</item>
          <item n="2">창가와 신소설</item>
        </list>
      </div>
    </front>
    
    <body>
      <div type="section" id="ch1">
        <head>제1장 신문학 태동기</head>
        <p>
          <s id="s1">
            <term type="concept">신문학</term>이 
            <term type="concept">창가</term>나 
            <term type="concept">신소설</term>의 형식으로 나오기 전에, 
            <interp value="affirmative" ana="번역의 선행적 역할 인정">
              일종의 번역행위가 앞서서 그 직접 준비의 과정으로 선행한 것
            </interp>을 짐작할 수 있다.
          </s>
        </p>
      </div>
    </body>
    
    <back>
      <div type="notes">
        <head>주석</head>
        <p>
          <s>원문 각주 및 편집자 주석</s>
        </p>
      </div>
    </back>
  </text>
</TEI>
```

## 유효성 검사

XML 문서가 이 스키마를 따르는지 검증하려면:

```bash
# xmllint 사용
xmllint --schema tei-criticism-schema.xsd your-document.xml --noout

# Python lxml 사용
from lxml import etree
schema = etree.XMLSchema(etree.parse('tei-criticism-schema.xsd'))
schema.validate(etree.parse('your-document.xml'))
```

## 주의사항

1. **body 필수**: `<text>` 내에 `<body>`는 반드시 포함되어야 합니다.
2. **순서 준수**: `front` → `body` → `back` 순서를 지켜야 합니다.
3. **interp의 ana 필수**: `<interp>` 요소의 `ana` 속성은 필수입니다.
4. **네임스페이스**: TEI 네임스페이스를 반드시 선언해야 합니다.

## 외부 데이터 연결

`ref` 속성을 통해 다음 외부 데이터베이스와 연결할 수 있습니다:

- [ISNI](https://isni.org/) - 국제 표준 이름 식별자
- [Wikidata](https://www.wikidata.org/)
- [한국민족문화대백과사전](https://encykorea.aks.ac.kr/)
- [한국사데이터베이스](https://db.history.go.kr/)

## 참고 자료

- [TEI P5 Guidelines](https://tei-c.org/release/doc/tei-p5-doc/en/html/index.html)
- [김바로 외, 『XML(TEI) with 인문학』](https://wikidocs.net/book/14569)

## 라이선스

이 스키마는 학술 연구 목적으로 자유롭게 사용할 수 있습니다.

## 저자

이병주 (공군사관학교 어문학과)

---

*이 스키마는 2023년 한국연구재단 인문사회분야 신진연구자지원사업(NRF-2023S1A5A8079304)의 지원을 받아 개발되었습니다.*
