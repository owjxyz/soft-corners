# Soft Corners

버튼·카드·프레임·이미지 래퍼에 부드러운 CSS 모서리를 적용하는 Codex 스킬입니다.

`corner-shape: superellipse(1.8)`을 사용하고, 기존보다 각져 보이지 않도록 `border-radius`를 보정합니다. `@supports` 기능 감지로 미지원 브라우저에서는 기존 디자인을 유지합니다.

## 설치

Codex에서 다음과 같이 요청하세요.

```text
$skill-installer https://github.com/owjxyz/soft-corners 스킬을 설치해줘.
```

설치 후 Codex를 재시작하면 스킬을 사용할 수 있습니다.

## 사용

```text
$soft-corners 버튼과 헤더 이미지에 주변 디자인과 어울리는 부드러운 모서리를 적용해줘.
```

대상 요소를 지정하면 기존 스타일과 모바일·hover·focus 상태를 확인하고 공통 CSS를 수정합니다. 기존 색상, 테마·다크모드 설정, 크기, 간격, 그림자는 유지합니다.

## 포함된 지침

- 일반적인 둥근 사각형의 반경을 약 1.75–1.8배로 보정한 뒤 시각적으로 조정
- 미지원 브라우저의 기존 반경 유지
- 이미지 래퍼 클리핑과 아이콘·포커스 표시 보호
- 테마 선택자 우선순위 충돌 확인
- 빌드 및 브라우저 검증

반경 배율은 시각적 출발점이며 모든 요소에 동일한 곡선을 보장하는 공식은 아닙니다.

실제 스킬 지침은 [SKILL.md](SKILL.md), 표시 정보는 [agents/openai.yaml](agents/openai.yaml)에 있습니다.
