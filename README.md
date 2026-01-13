# 현대문학비평 XML 데이터 구축 (Korean Modern Literary Criticism XML Data)

디지털 인문학 연구를 위한 한국 현대문학비평 XML 데이터 구축 방법론

## 프로젝트 소개

본 프로젝트는 한국 현대문학비평 텍스트를 XML 기반의 구조화된 데이터로 변환하기 위한 방법론과 도구를 제공합니다. TEI(Text Encoding Initiative) P5 가이드라인을 준용하되, 문학비평의 특수성을 반영한 맞춤형 스키마(XSD)를 설계하였습니다.

### 주요 특징

- **TEI P5 기반**: 국제 표준을 따르는 XML 구조
- **비평 특화 마크업**: 평가적 언술(`<interp>`)과 인용(`<quote>`) 요소 지원
- **외부 데이터 연결**: ISNI, Wikidata, 한국민족문화대백과사전 등과의 연계성 확보
- **확장 가능한 구조**: 시맨틱 데이터베이스로의 확장 가능

## 마크업 요소

### 핵심 요소

| 요소 | 기능 | 주요 속성 |
|------|------|--------|
| `<persName>` | 인명 표기 (작가, 비평가 등) | `role`, `xml:id`, `ref` |
| `<title>` | 작품명, 논문명, 잡지명 | `level`, `type` |
| `<term>` | 개념어, 사조, 비평 용어 | `type`, `xml:id` |
| `<quote>` | 비평문, 작품 인용 | `type`, `genre`, `source` |
| `<interp>` | 비평적 평가, 태도 명시 | `value`, `ana` |

### 평가 속성값 (`<interp>`)

- `affirmative`: 긍정적 평가
- `neutral`: 중립적 서술
- `critical`: 부정적 평가

## 파일 구조

```
├── tei-criticism-schema.xsd    # XML 스키마 정의
├── examples/                    # 예시 XML 파일
│   ├── baekchul_sample.xml     # 백철 『조선신문학사조사』 샘플
│   └── kimwoochang_sample.xml  # 김우창 비평 샘플
├── analysis/                    # 분석 결과
│   └── tagging_frequency.csv   # 태깅 요소 빈도 분석
└── README.md
```

## 사용 예시

### 인명 마크업

```xml
<persName 
  role="critic" 
  xml:id="isni-0000000084484348" 
  ref="https://encykorea.aks.ac.kr/Article/E0047762">
  임화
</persName>
```

### 평가 마크업

```xml
<interp value="affirmative" ana="번역이 신문학 형성의 준비 과정이었다는 긍정적 평가">
  그 직접 준비의 과정으로 선행한 것을 짐작할 수 있는 것이다.
</interp>
```

### 인용 마크업

```xml
<quote type="direct" genre="critic" source="김수영">
  "시란 자기 존재의 불안이다."
</quote>
```

## 활용 방안

1. **XPath/XQuery 분석**: 문맥적 탐색 및 데이터 추출
2. **네트워크 분석**: 비평가-작가 간 영향 관계 시각화
3. **개념사 연구**: 비평 용어의 역사적 변천 추적
4. **정전 형성 연구**: 문학사 내 작가/작품 평가 패턴 분석

## 외부 데이터 연결

본 스키마는 다음 외부 데이터베이스와의 연결을 지원합니다:

- [ISNI (International Standard Name Identifier)](https://isni.org/)
- [Wikidata](https://www.wikidata.org/)
- [한국민족문화대백과사전](https://encykorea.aks.ac.kr/)
- [네이버 지식백과](https://terms.naver.com/)

## 기술 스택

- XML 1.0
- XSD (XML Schema Definition)
- TEI P5 Guidelines
- XPath / XQuery

## 참고 문헌

- TEI Consortium, *TEI P5: Guidelines for Electronic Text Encoding and Interchange*
- 김바로 외, 『XML(TEI) with 인문학』, 위키독스, 2025
- 김현, 「디지털 인문학과 고문헌 자료 연구」, 『열상고전연구』, 2016

## 인용

본 프로젝트를 연구에 활용하실 경우 다음과 같이 인용해 주세요:

```
이병주, 「현대문학비평 XML 데이터 구축과 활용 방안: 디지털 인문학 연구를 위한 방법론 모색」, 
『한국시학연구』 제83호, 한국시학회, 2025.
```

## 라이선스

본 프로젝트의 스키마와 방법론은 학술 연구 목적으로 자유롭게 사용할 수 있습니다.  
단, 원문 데이터는 저작권법의 보호를 받으므로 별도의 허가가 필요합니다.

## 연락처

- **저자**: 이병주 (공군사관학교 어문학과)
- **GitHub**: [https://github.com/ByeongjooLee/xmldata](https://github.com/ByeongjooLee/xmldata)

## 감사의 글

이 연구는 2023년 대한민국 교육부와 한국연구재단의 인문사회분야 신진연구자지원사업의 지원을 받아 수행되었습니다. (NRF-2023S1A5A8079304)
