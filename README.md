# Yves Saint Laurent 가격 추적기

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.co.kr)
[![Yves Saint Laurent Price Tracker](https://img.shields.io/badge/Yves%20Saint%20Laurent%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.co.kr/products/insights/price-tracker/ysl)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.co.kr/products/insights/price-tracker/ysl)

프랑스 럭셔리 패션 및 뷰티 브랜드인 Yves Saint Laurent의 실시간 가격 추적. 시작하는 방법은 두 가지입니다: **완전 관리형** 인텔리전스 플랫폼 또는 자체 파이프라인을 구축할 수 있는 **셀프서비스 API**.

---

## 옵션 1: Bright Insights - AI 기반 가격 추적 (권장)

**[Bright Insights](https://brightdata.co.kr/products/insights/price-tracker/ysl)**는 Bright Data의 완전 관리형 리테일 인텔리전스 플랫폼입니다. scraper를 구축할 필요도, 인프라를 유지할 필요도 없습니다. 구조화되고 분석 준비가 완료된 가격 데이터가 대시보드, 데이터 피드 또는 BI 도구로 바로 전달됩니다.

**팀이 Bright Insights를 선택하는 이유:**
- 🚀 **설정 불필요** - 바로 사용할 수 있는 대시보드와 데이터 피드로 몇 분 안에 시작
- 🤖 **AI 기반 추천** - 대화형 AI assistant가 수백만 개의 데이터 포인트를 즉시 실행 가능한 인사이트로 전환
- ⚡ **실시간 모니터링** - 시간별~일별 새로고침 주기와 즉시 알림(email, Slack, webhook)
- 🌍 **무제한 확장성** - 모든 웹사이트, 모든 지역, 모든 새로고침 빈도 지원
- 🔗 **Plug-and-play 통합** - AWS, GCP, Databricks, Snowflake 등과 연동
- 🛡️ **완전 관리형** - Bright Data가 schema 변경, 사이트 업데이트, 데이터 품질을 자동으로 처리

**주요 사용 사례:**
- ✅ Yves Saint Laurent의 **희귀 및 한정판 가격** 모니터링
- ✅ 사이즈 및 색상별 **재고 현황**을 실시간으로 추적
- ✅ 리테일 가격 대비 **리셀 프리미엄** 검증
- ✅ MAP 정책 준수 여부를 모니터링하고 가격 위반 감지
- ✅ 경쟁사 프로모션 및 프로모션 동향 추적
- ✅ 정제되고 표준화된 데이터를 동적 가격 책정 알고리즘 또는 AI 모델에 직접 공급

> **월 $250부터 - [맞춤 견적 받기 →](https://brightdata.co.kr/products/insights/price-tracker/ysl)**

---

## 옵션 2: Web Scraper API를 통한 셀프서비스

직접 파이프라인을 구축하고 싶으신가요? Bright Data의 **Web Scraper API**를 사용하면 proxy나 scraping 인프라를 관리하지 않고도 Yves Saint Laurent 제품 데이터(가격, 재고, 리뷰 등)에 programmatic하게 접근할 수 있습니다.

### 사전 요구 사항

- Python 3.9 이상
- [Bright Data account](https://brightdata.co.kr) (무료 체험 가능)
- Bright Data **API token** ([발급 방법](https://docs.brightdata.co.kr/general/account/account-settings#api-token))
- Yves Saint Laurent 제품용 Bright Data **Web Scraper ID** ([Web Scrapers control panel에서 확인](https://brightdata.co.kr/cp/scrapers))

### 설정

1. **이 repository 복제**

   ```bash
   git clone https://github.com/bright-kr/ysl-price-tracker.git
   cd ysl-price-tracker
   ```

2. **의존성 설치**

   ```bash
   pip install -r requirements.txt
   ```

3. **자격 증명 구성**

   `.env.example`을 `.env`로 복사한 뒤 값을 입력하세요:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Web Scraper ID 찾기**
   > [Bright Data Control Panel](https://brightdata.co.kr/cp/scrapers)에 로그인한 후 **Web Scrapers**로 이동하여
   > "Yves Saint Laurent"를 검색하고 Web Scraper ID를 복사하세요(형식: `gd_xxxxxxxxxxxx`).

---

## 사용 방법

### 1. URL로 특정 제품 추적

Yves Saint Laurent 제품 URL 목록을 전달하여 구조화된 가격 데이터를 가져옵니다:

```python
from price_tracker import track_prices

urls = [
    "https://www.ysl.com/en/products/sample-product-123456",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

또는 직접 실행:

```bash
python price_tracker.py
```

### 2. 키워드로 제품 검색

키워드 검색과 일치하는 제품을 찾습니다:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. 카테고리 URL로 제품 탐색

Yves Saint Laurent 카테고리 페이지의 모든 제품을 수집합니다:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://ysl.com/category/example",
    limit=100,
)
```

---

## 출력 필드

각 결과 레코드에는 다음 필드가 포함됩니다:

| Field | Description |
|-------|-------------|
| `url` | 제품 페이지 URL |
| `title` | 제품명 |
| `brand` | 브랜드/하우스 |
| `price` | 소매 가격 |
| `currency` | 통화 코드 |
| `in_stock` | 재고 여부 |
| `color` | 색상 |
| `size` | 사용 가능한 사이즈 |
| `material` | 사용된 소재 |
| `sku` | SKU / 참조 번호 |
| `images` | 제품 이미지 |
| `description` | 제품 설명 |
| `timestamp` | 수집 타임스탬프 |

### 샘플 출력

```json
[
  {
    "url": "https://www.ysl.com/en/products/sample-product-123456",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://ysl.com/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## 고급 옵션

`trigger_collection()` 함수는 데이터 수집을 제어하기 위한 선택적 파라미터를 지원합니다:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | 반환할 최대 레코드 수 |
| `include_errors` | boolean | `true` | 결과에 오류 리포트 포함 |
| `notify` | string (URL) | - | 스냅샷 준비 완료 시 호출할 webhook URL |
| `format` | string | `json` | 출력 형식: `json`, `csv` 또는 `ndjson` |

옵션 사용 예시:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.ysl.com/en/products/sample-product-123456"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## 리소스

- 🌟 [Yves Saint Laurent Price Tracker - Bright Insights (Managed)](https://brightdata.co.kr/products/insights/price-tracker/ysl)
- 🔧 [Yves Saint Laurent Scraper API](https://brightdata.co.kr/products/web-scraper/ysl)
- 📖 [Bright Data Web Scraper API Documentation](https://docs.brightdata.co.kr/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapers Control Panel](https://brightdata.co.kr/cp/scrapers)
- 🔑 [API token 발급 방법](https://docs.brightdata.co.kr/general/account/account-settings#api-token)
- 🌐 [Bright Data 홈페이지](https://brightdata.co.kr)

---

*[Bright Data](https://brightdata.co.kr)로 구축 - 업계를 선도하는 웹 데이터 플랫폼.*