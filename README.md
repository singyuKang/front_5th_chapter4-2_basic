# 과제 체크포인트

## 배포링크
https://front-5th-chapter4-2-basic-theta.vercel.app/

## 과제 요구사항 만족

- [x] 배포 후 url 제출
- [x] 성능 개선 보고서 작성

- [x] Lighthouse 점수 이해
- [x] Core Web Vital 이해

## 과제 셀프회고


## CORS 에러

과제 최적화와 직접적인 관련은 없지만, 에러를 만났던 상황을 기록하기 위해 정리하였습니다.

### 에러 상황
`index.html` 파일을 브라우저에서 열었을 때 `CORS` 에러가 발생했습니다.
에러 메시지는 익숙했지만 정확한 원인을 몰라 관련 내용을 조사하였습니다.

### CORS란?
**CORS(Cross-Origin Resource Sharing)**는 다른 출처(origin) 간의 리소스 공유를 제한하는 브라우저의 보안 정책입니다.
한 출처(origin)에서 실행 중인 웹 애플리케이션이 다른 출처의 리소스에 접근하려 할 때, 명시적인 허용(CORS 설정)이 없다면 브라우저는 이를 차단합니다.

### 같은 출처(Same-Origin)의 기준
브라우저는 프로토콜(Protocol), 도메인(Domain), **포트 번호(Port)**의 세 가지가 모두 같을 때만 **같은 출처(same-origin)**로 간주합니다.

예를 들어

```
http://localhost:8000
http://localhost:3000
```
위 두 URL은 포트 번호가 다르므로 **다른 출처**로 간주됩니다.

반대로, 아래 두 URL은 프로토콜, 도메인, 포트 번호가 모두 같기 때문에 **같은 출처**입니다.

```
http://localhost:8000/page1.html
http://localhost:8000/page2.html
```

요약하면

**출처 = 프로토콜 + 도메인 + 포트 번호**
이 세 요소 중 하나라도 다르면 다른 출처로 인식되어 CORS 정책이 적용됩니다.

브라우저 입장에서 `file://singyuKangOne/index.html` 과 `file://singyuKangTwo/index.html` 은 서로 **다른 출처**로 인식됩니다.

하나의 파일에서 다른 디렉토리의 파일을 불러오면 **Cross-Origin** 요청이 되며,

이때 CORS 정책에 의해 리소스 요청이 차단되어 에러가 발생합니다.

## 과제 초기 성능
<img width="716" height="655" alt="Image" src="https://github.com/user-attachments/assets/6641aecc-456e-4d70-98ab-95d118542261" />

<h3>🎯 Lighthouse 점수</h3>

카테고리 | 점수 | 상태
-- | -- | --
Performance | 72% | 🟠
Accessibility | 82% | 🟠
Best Practices | 75% | 🟠
SEO | 82% | 🟠
PWA | 0% | 🔴


<h3>📊 Core Web Vitals (2024)</h3>

메트릭 | 설명 | 측정값 | 상태
-- | -- | -- | --
LCP | Largest Contentful Paint | 14.78s | 🔴
INP | Interaction to Next Paint | N/A | 🟢
CLS | Cumulative Layout Shift | 0.011 | 🟢



## 이미지 리소스 최적화: JPG, PNG → WebP 변경

### 변경 전 코드
```html
<img class="desktop" src="images/Hero_Desktop.jpg" />
<img class="mobile" src="images/Hero_Mobile.jpg" />
<img class="tablet" src="images/Hero_Tablet.jpg" />
```

### 변경 후 코드
```html
<img class="desktop" src="images/Hero_Desktop.webp" />
<img class="mobile" src="images/Hero_Mobile.webp" />
<img class="tablet" src="images/Hero_Tablet.webp" />
```
기존 JPG 이미지를 **WebP 포맷**으로 변환하여 적용하였습니다.

**WebP**는 더 작은 용량으로 비슷한 이미지 품질을 유지할 수 있어 페이지 로딩 속도 향상!

<img width="580" height="565" alt="Image" src="https://github.com/user-attachments/assets/9bd05cec-4b54-4586-9ab3-8ab64e1e71cb" />


### 성능 개선 결과

📊 Core Web Vitals (2024)
| 메트릭 | 설명 | 측정값 | 상태 |
|--------|------|--------|------|
| LCP | Largest Contentful Paint | 9.61s | 🔴 |
| INP | Interaction to Next Paint | N/A | 🟢 |
| CLS | Cumulative Layout Shift | 0.011 | 🟢 |

LCP (Largest Contentful Paint): **14.7초 → 9.61초**로 개선

Lighthouse 성능 점수: **81점 → 96점**으로 상승

이미지 포맷 변경만으로도 페이지의 초기 로딩 성능에 직접적인 영향을 미침을 확인할 수 있었습니다.

## 폰트 최적화 

<img width="202" height="177" alt="Image" src="https://github.com/user-attachments/assets/700fb4a6-0926-4c48-86f1-9c6edc130768" />

```javascript
@font-face {
  font-family: "Heebo";
  src: url("fonts/Heebo-Light.woff2") format("woff");
  font-display: swap;
  font-weight: 300;
  font-style: light;
}

@font-face {
  font-family: "Heebo";
  src: url("fonts/Heebo-Regular.woff2") format("woff");
  font-display: swap;
  font-weight: 400;
  font-style: normal;
}

@font-face {
  font-family: "Heebo";
  src: url("fonts/Heebo-Medium.woff2") format("woff");
  font-display: swap;
  font-weight: 600;
  font-style: medium;
}

@font-face {
  font-family: "Heebo";
  src: url("fonts/Heebo-Bold.woff2") format("woff");
  font-display: swap;
  font-weight: 700;
  font-style: bold;
}
```

기존에는 구글 폰트 링크를 통해 외부에서 폰트를 불러왔으나, 성능 최적화를 위해 폰트를 **자체 호스팅**하는 방식으로 변경했습니다. 

특히, **woff2 파일 형식**은 **ttf 형식**에 비해 **더 높은 압축률**을 제공하여 파일 크기를 줄이고, 로딩 시간을 단축시킵니다.

### 📊 Core Web Vitals (2024)
| 메트릭 | 설명 | 측정값 | 상태 |
|--------|------|--------|------|
| LCP | Largest Contentful Paint | 8.78s | 🔴 |
| INP | Interaction to Next Paint | N/A | 🟢 |
| CLS | Cumulative Layout Shift | 0.011 | 🟢 |


### 이미지 렌더링 방식 변경

기존에는 HTML에서 각 디바이스별 이미지를 <img> 태그로 모두 불러온 뒤, CSS에서 display: none으로 보이지 않는 **이미지를 숨기**는 방식을 사용했습니다.
```javascript
section.hero img.desktop {
  display: none;
}
section.hero img.tablet {
  display: initial;
}
```
- 실제로는 모든 이미지를 로딩하지만, 화면에 보이는 이미지만 렌더링

- 불필요한 이미지도 다운로드

아래와 같이 `<picture> 요소`를 사용해 미디어 쿼리 기반의 **조건부 이미지 로딩**으로 구조를 변경했습니다.

```javascript
<picture>
  <source media="(max-width: 576px)" srcset="images/Hero_Mobile.webp" />
  <source media="(min-width: 577px) and (max-width: 960px)" srcset="images/Hero_Tablet.webp" />
  <img
    src="images/Hero_Desktop.webp"
    width="900"
    height="600"
    alt="Hero Desktop"
    fetchpriority="high"
    loading="eager"
  />
</picture>
```

브라우저가 현재 화면 크기에 맞는 **하나의 이미지**만 선택적으로 로드 -> 불필요한 이미지 리소스 낭비가 줄어듦

### 📊 Core Web Vitals (2024)
| 메트릭 | 설명 | 측정값 | 상태 |
|--------|------|--------|------|
| LCP | Largest Contentful Paint | 3.38s | 🟠 |
| INP | Interaction to Next Paint | N/A | 🟢 |
| CLS | Cumulative Layout Shift | 0.001 | 🟢 |

| 항목      | 설명                       | 변경 전  | 상태    | 변경 후            |
| ------- | ------------------------ | ----- | ----- | --------------- |
| **LCP** | Largest Contentful Paint | 8.78초 | 🔴 느림 | **3.38초로 개선** ✅ |

브라우저에 맞는 이미지 최적화로 LCP가 가장 큰폭으로 감소하였습니다

## 스크립트 로딩 최적화

### 변경전

```javascript
<script type="text/javascript" charset="UTF-8">
  cookieconsent.run({
    ...
  });
</script>
```
기존에는 HTML 파싱 도중에 스크립트를 즉시 실행을 하였는데 이로 인해 렌더링이 차단이 됩니다.

```javascript
<script type="text/javascript" defer>
  document.addEventListener("DOMContentLoaded", function () {
    cookieconsent.run({
      ...
    });
  });
</script>
```
defer 속성 추가로 HTML 파싱이 끝난 후 스크립트를 실행하도록 변경 -> 초기 화면 표시 속도 개선

<img width="767" height="672" alt="Image" src="https://github.com/user-attachments/assets/105fc462-3199-4b5e-81f0-5c06cb90ec65" />

### 📊 Core Web Vitals (2024)
| 메트릭 | 설명 | 측정값 | 상태 |
|--------|------|--------|------|
| LCP | Largest Contentful Paint | 0.8s | 🟢 |
| INP | Interaction to Next Paint | N/A | 🟢 |
| CLS | Cumulative Layout Shift | 0.001 | 🟢 |

## 웹 접근성 및 SEO 최적화

### meta description 추가
```javascript
<meta
  name="description"
  content="최신 VR 헤드셋과 첨단 기술 제품을 만나보세요. 고품질 가상현실 체험을 위한 프리미엄 VR 기기와 액세서리를 합리적인 가격에 제공합니다."
/>
```
검색 엔진 결과 페이지(SERP)에서 웹페이지 요약문으로 활용

사용자 및 검색 엔진에 페이지 내용을 명확히 전달

### 모든 이미지 alt 속성 추가
```javascript
<img
  src="images/menu_icon.webp"
  alt="menu-icon"
  width="24"
  height="24"
/>
```
검색 엔진이 이미지를 인식할 수 있어 SEO 측면에서도 긍정적인 효과

## Lighthouse & PageSpeed Insight 측정 결과

###  Local 환경 – Lighthouse 측정 결과
<img width="767" height="672" alt="Image" src="https://github.com/user-attachments/assets/95e3131a-34f1-42db-9236-76f3b38ddab2" />
로컬 환경에서 Chrome DevTools의 Lighthouse로 성능 측정

### Local 환경 – PageSpeed Insight 결과
<img width="1163" height="666" alt="Image" src="https://github.com/user-attachments/assets/12cbc378-1adf-42d4-a600-db0b785bdf9a" />

### 배포 환경 – PageSpeed Insight 결과
<img width="1066" height="638" alt="Image" src="https://github.com/user-attachments/assets/c7f141fa-53b7-41b5-a67d-a430fb14d134" />




## 리뷰 받고 싶은 내용

이미지 최적화를 진행하며 WebP 포맷을 적용했지만, AVIF라는 더 높은 압축률을 가진 포맷도 존재한다는 것을 알게 되었습니다.
현업에서는 AVIF 포맷을 얼마나 자주 사용하는지, 그리고 코치님만의 선택 기준이나 원칙이 있는지 궁금합니다.

이번 과제처럼 Lighthouse나 PageSpeed Insight를 활용해 성능 측정을 정리했는데,
실제 실무에서도 이와 같은 방식으로 최적화 과정을 평가하고 공유하는지 알고 싶습니다.
