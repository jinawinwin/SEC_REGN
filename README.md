<p align="center">
  <a href="https://jinawinwin.github.io/SEC_REGN/">
    <img src="assets/regeneron-badge.svg" alt="Regeneron — 대시보드 바로가기" width="300">
  </a>
  <br>
  <a href="https://jinawinwin.github.io/SEC_REGN/"><b>🔗 대시보드 바로가기</b></a>
</p>

# Regeneron Pharmaceuticals SEC Filings Dashboard

SEC EDGAR에 공시된 Regeneron Pharmaceuticals, Inc. (NASDAQ: REGN, CIK 0000872589)의 10-K·10-Q XBRL 데이터를 수집해 2010년 이후 연간·반기·분기 재무자료와 바이오 기업 특화 R&D 지표를 분석합니다.

**대시보드:** https://jinawinwin.github.io/SEC_REGN/

마지막 데이터 갱신: <!-- UPDATED:START -->2026-10-31 (latest 10-K/10-Q on file: 2026-10-30)<!-- UPDATED:END -->

## 대시보드 구성

| 영역 | 내용 |
|---|---|
| 상단 | Revenue, Operating income, Net income, FCF, 최근 분기 매출 KPI |
| Figures | 연간 실적, 분기 매출 성장률, 영업·순이익·FCF 마진, R&D / Revenue, CapEx / Revenue, 현금흐름, 재무구조, 손익 Waterfall |
| R&D 분석 | R&D 비용, 매출 대비 R&D 투자 비중, 연간 추이 |
| 하단 | **연간 / 반기 / 분기** 재무제표와 비율 테이블 |
| 최하단 | **미국 상장 바이오·제약 Peer firms** 비교 |
| 우측 패널 | PDF 저장 및 기간 선택형 Excel 저장 |

## 데이터 저장 위치

| 경로 | 설명 |
|---|---|
| `data/raw/regn_selected_facts.json` | SEC companyfacts에서 선택한 Regeneron XBRL facts |
| `data/raw/regn_filings.json` | 최근 10-K / 10-Q 공시 목록 |
| `data/annual.csv` · `half_year.csv` · `quarterly.csv` | 연간·반기·분기 가공 데이터 (USD millions, EPS는 USD) |
| `data/peers.csv` | Regeneron 및 Peer 기업 최신 회계연도 비교 |
| `docs/data/dashboard.json` | 대시보드가 읽는 데이터 파일 |

**데이터 범위:** SEC companyfacts의 표준 XBRL 태그를 기반으로 합니다. 회사의 제품 매출·협업 매출 세부 분해, 임상단계별 파이프라인, 개별 프로그램 R&D는 모든 기간에 동일한 표준 태그로 제공되지 않으므로 기본 대시보드 재무자료와 별도로 해석해야 합니다. Regeneron의 협업 매출에는 제조 관련 원가가 별도 공시되므로 표준 원가 태그만으로 전체 매출총이익률을 추정하지 않습니다.

## 자동 업데이트 (매월 1일)

`.github/workflows/update.yml`이 **매월 1일 00:00 UTC (한국시간 09:00)** 에 다음을 수행합니다.

1. 재무 파이프라인 단위 테스트 실행
2. SEC EDGAR에서 Regeneron 및 Peer 기업 데이터 수집
3. 2010년 이후 연간·반기·분기 데이터와 비율 계산
4. CSV, 원천 JSON, 대시보드 JSON, README 갱신 및 커밋
5. GitHub Pages 자동 배포

Actions 탭의 **Update Regeneron SEC data & deploy dashboard → Run workflow**로 수동 실행할 수 있습니다.

### 최초 1회 Secret 설정

저장소 *Settings → Secrets and variables → Actions → Secrets*에서 다음 Repository Secret을 등록하세요.

- 이름: `SEC_USER_AGENT`
- 값: `SEC_REGN Dashboard contact@실제이메일주소`

이메일만 입력하지 말고, 서비스/프로젝트 식별자와 실제 연락 가능한 이메일을 함께 입력합니다. 공개 저장소이므로 Variable이 아닌 Secret을 사용합니다.

## Global peer firms

Peer 기업은 미국 상장 바이오·제약 기업으로 구성했습니다. 실제 SEC entityName이 설정된 CIK와 일치하는 경우에만 수집합니다.

<!-- PEERS:START -->
| Company | Ticker | Region | Why a peer | FY end | Revenue (m) | Op. margin | Net margin | R&D / rev | CapEx / rev | Ccy |
|---|---|---|---|---|---:|---:|---:|---:|---:|---|
| **Regeneron** | REGN | US | Subject company (reference row) | 2025-12-31 | 14,343 | 24.9% | 31.4% | 40.8% | 6.3% | USD |
| Amgen | AMGN | US | Large-cap biotechnology; biologics, oncology and inflammation | 2025-12-31 | 36,751 | 24.7% | 21.0% | 19.8% | 5.1% | USD |
| Gilead Sciences | GILD | US | Antiviral franchises, oncology and cell therapy | 2025-12-31 | 29,443 | 34.0% | 28.9% | 19.7% | 1.9% | USD |
| Vertex Pharmaceuticals | VRTX | US | Specialty biotech with commercial products and pipeline expansion | 2025-12-31 | 12,001 | 34.8% | 32.9% | 32.6% | 3.6% | USD |
| AbbVie | ABBV | US | Immunology, oncology and large-scale pharmaceutical R&D | 2025-12-31 | 61,160 | 24.6% | 6.9% | 14.9% | 2.0% | USD |
| Bristol Myers Squibb | BMY | US | Oncology, immunology and innovative medicines | 2025-12-31 | 48,194 | — | 14.6% | 20.6% | 2.7% | USD |
| Eli Lilly | LLY | US | Biopharma growth benchmark in cardiometabolic and oncology medicines | 2025-12-31 | 65,179 | — | 31.7% | 20.5% | — | USD |
| Merck & Co. | MRK | US | Large-cap pharmaceutical company with oncology and vaccine franchises | 2025-12-31 | 65,011 | — | 28.1% | 24.3% | 6.3% | USD |
| Pfizer | PFE | US | Global pharmaceutical scale, vaccines and oncology | 2025-12-31 | 62,579 | — | 12.4% | 16.7% | 4.2% | USD |
| Biogen | BIIB | US | Specialty biotechnology focused on neuroscience and rare disease | 2025-12-31 | 9,891 | — | 13.1% | 18.0% | 1.6% | USD |
| Alnylam Pharmaceuticals | ALNY | US | RNAi platform and research-intensive commercial biotechnology | 2025-12-31 | 3,714 | 13.5% | 8.4% | 35.5% | 1.6% | USD |
<!-- PEERS:END -->

비교 대상: Amgen, Gilead Sciences, Vertex Pharmaceuticals, AbbVie, Bristol Myers Squibb, Eli Lilly, Merck, Pfizer, Biogen, Alnylam Pharmaceuticals.

## 로컬 실행

```bash
SEC_USER_AGENT="SEC_REGN Dashboard contact@example.com" python scripts/fetch_sec.py
python -m unittest discover -s tests -v
python -m http.server -d docs 8000
```

## 분석 유의사항

- 기준 기업: Regeneron Pharmaceuticals, Inc. (CIK 0000872589), 회계연도 종료일 12월 31일.
- 기간은 2010년 이후로 제한합니다. SEC XBRL facts는 이후 제출된 정정·비교 공시를 반영할 수 있습니다.
- R&D / Revenue는 SEC 표준 R&D expense 태그 기준이며, 취득 IPR&D의 별도 인식 여부는 기간별 태그를 확인해야 합니다.
- 매출은 제품·협업·기타 매출을 포함하는 회사 전체 매출입니다. 제품별 매출 및 파이프라인 단계별 성과는 별도 공시 분석이 필요합니다.
- 본 자료는 정보 제공 목적이며 투자 자문이 아닙니다.
