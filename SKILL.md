---
name: soft-corners
description: Apply soft CSS superellipse corners to requested buttons, cards, frames, or image wrappers, compensating border radii and preserving existing styles in unsupported browsers. Use for corner-shape, squircle, continuous corners, or 부드러운 모서리 requests in web UI; not raster image editing.
---

# 부드러운 모서리

기본 형태는 `corner-shape: superellipse(1.8)`이다. 기존 디자인의 둥근 정도를 유지하면서 곡선을 부드럽게 만든다. 사용자가 다른 값을 지정하면 그 값을 따른다.

## 적용

1. 대상 요소의 실제 DOM과 공통 스타일을 읽고, 기존 `border-radius`, 모바일·상태별 규칙과 최종 계산값을 확인한다. 공통 스타일 한 곳에서 요청한 범위에만 적용한다.
2. 기존 CSS를 미지원 브라우저의 기본값으로 남긴다. `corner-shape`와 보정 반경 모두 `@supports (corner-shape: superellipse(1.8))` 안에 둔다. 브라우저 이름이나 사용자 에이전트로 분기하지 않는다.
3. 같은 반경에 `superellipse(1.8)`만 추가하면 더 각져 보일 수 있다. 일반적인 둥근 사각형은 기존 반경의 약 **1.75–1.8배**를 출발점으로 삼고 실제 크기에서 조정한다. 이는 시각적 경험값이며 수학적으로 동일한 곡선이라는 뜻은 아니다. 예: `11px → 20px`, 모바일 `8px → 14px`, 카드 `20px → 36px`. 비대칭 반경에서 의도적으로 각진 0인 모서리는 유지한다. 사용자가 직사각형 요소를 둥글게 만들도록 요청하면 요소 크기에 맞는 새 반경을 기능 블록 안에 지정한다. 원형·캡슐형에는 배율을 기계적으로 적용하지 않는다.
4. 이미지·영상이 모서리 밖으로 나오면 래퍼에서 클리핑한다. 필요한 래퍼에만 `overflow: hidden`을 적용하고, 팝오버·드롭다운·포커스 표시가 잘리지 않는지 확인한다. 내부 로고·아이콘을 일괄 선택하지 않는다.
5. 테마가 반경을 덮어쓰면 개발자 도구에서 승리하는 규칙을 찾고, 공통 override의 순서나 선택자 우선순위를 최소한으로 조정한다. 불필요한 `!important`, JS, SVG 마스크, 폴리필을 추가하지 않는다. 기존 색상, 테마·다크모드 설정, 크기, 간격, 그림자는 유지한다.

## 예시

아래 기본 규칙은 기존 디자인을 나타낸다. 실제 작업에서는 기존 규칙을 재사용한다.

```css
.button { border-radius: 11px; }
@media (max-width: 620px) {
  .button { border-radius: 8px; }
}

@supports (corner-shape: superellipse(1.8)) {
  .button {
    corner-shape: superellipse(1.8);
    border-radius: 20px;
  }
  @media (max-width: 620px) {
    .button { border-radius: 14px; }
  }
}
```

## 확인

프로젝트의 CSS/사이트 빌드를 실행한다. 지원 브라우저에서 `CSS.supports('corner-shape', 'superellipse(1.8)')`와 계산된 `corner-shape`, `border-radius`를 확인한다. 데스크톱·모바일, hover·focus 상태와 이미지 클리핑을 눈으로 확인한다. 기능 블록을 끄거나 미지원 브라우저에서 기존 모양이 유지되는지 확인한다. 기존 빌드 문제를 발견하면 모서리 변경과 구분해 보고한다. 요청하지 않은 게시·배포까지 확장하지 않는다.

참고: [MDN corner-shape](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/corner-shape). 지원 여부는 작업 시점의 기능 감지로 판단한다.
