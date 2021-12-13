# 시작하기

## 기본 사용

[첫 번째 예제](http://6pac.github.io/SlickGrid/examples/example1-simple.html)에서 가져온 SlickGrid의 기본입니다.

```javascript
const slickgrid = new Slick.Grid(container, rows, columns, options);
```

SlickGrid를 초기화 및 렌더링 하고 인터페이스를 `slickgrid` 변수에 할당합니다. 이제 우리는 `slickgrid.someMethod()`를 사용하여 상호작용 할 수 있습니다.

## Container

`container`(Element 또는 jQuery selector)는 그리드가 생성될 HTML 요소를 가리킵니다. 일반적으로 빈 `<div>`가 됩니다. `<div>`에는 CSS 또는 스타일 특성을 통해 지정된 명시적 치수(높이 및 너비)가 있어야 합니다. 그리드는 사용 가능한 모든 공간을 차지하도록 크기가 조정됩니다.

## Rows

`row`는 데이터 객체의 배열입니다. 예:

```javascript
const rows = [
	{
		field_1: "value1",
		field_2: "value2"
	}, {
		field_1: "value3",
		field_2: "value4"
	}
];
```

그리드에 데이터를 제공하는 방법은 [여기](https://github.com/mleibman/SlickGrid/wiki/Providing-data-to-the-grid)서 더 자세히 설명합니다.

그리드를 참조할 때 직접 수정할 수 있지만 그리드는 데이터가 언제 변경되었는지 알 수 없으므로 다음과 같이 다시 렌더링 해야합니다:

```jsx
slickgrid.invalidate();
```

이렇게 하면 모든 행이 강제로 소멸되고 다시 생성되지만 그리드는 뷰포트의 행(작은 버퍼 포함)만 렌더링하므로 이 메소드의 성능은 일정하며 데이터셋의 행 수에 의존하지 않습니다. 그러나 효율성을 높이려면 다시 렌더링해야 하는 행과 행수가 변경되었는지 여부를 그리드에 정확하게 알릴 수 있습니다:

```jsx
slickgrid.invalidateRows([4, 7]);
slickgrid.updateRowCount();
slickgrid.render();
```

이렇게 하면 행 수가 업데이트될 뿐만 아니라 그리드 렌더러 4행과 7행(0부터 시작)이 됩니다.(새 행이 렌더링 되고 데이터 집합에서 행이 더 이상 제거되지 않음)

이것은 매우 효율적인 UI 업데이트를 가능하게 하는 SlickGrid의 주요 강점 중 하나입니다.

## Columns

`columns`은 최소 다음의 필드를 포함하는 객체의 배열입니다.

* `name` - 보기에 표시할 이름입니다.
* `field` - 데이터 행 객체에서 사용되는 필드 이름입니다.
* `id` - 동일한 필드를 읽는 열을 두 개 이상 설정할 수 있는 모델의 각 열에 대한 고유 식별자 입니다.

기타 필드는 다음과 같습니다:

```jsx
resizable
sortable
selectable
focusable
width
minWidth
maxWidth
rerenderOnResize
headerCssClass
formatter
editor
etc.
```

예시:

```jsx
const columns = [
    {
        name: "Address",
        field: "address",
        id: "address",  // 대부분의 경우 field와 id값은 동일합니다.
        sortable: true
    }, 
    {
        name: "Rating, in %",
        field: "rating", // 이 열과 다음 열은 동일한 데이터를 읽지만 다른 방식으로 표시할 수 있습니다.
        id: "rating_percent",
        resizable: false
    }, 
    {
        name: "Rating, in stars",
        field: "rating",
        id: "rating_stars"
    }
];
```

## Options

option을 사용하면 [추가 옵션](https://github.com/6pac/SlickGrid/wiki/Grid-Options)을 지정할 수 있습니다.

## Events

SlickGrid는 자체적인 간단한 이벤트 구현체가 있습니다. 이벤트를 구독하려면 `event.subscribe()`를 호출하고 브라우저 이벤트가 포함된 이벤트 객체와 그리드에서 전달된 데이터가 포함된 추가 `arg` 개체라는 두 가지 매개 변수를 사용하는 함수를 전달합니다.

예:

```jsx
slickgrid.onDblClick.subscribe((e, args) => {
    const { item } = args; // name, field, id 등을 포함하는 객체
});
```

전체 목록은 [이벤트](https://github.com/6pac/SlickGrid/wiki/Grid-Events)를 참조하십시오.

## Basic sorting

`onSort` 메서드를 통해 다음을 수행할 수 있습니다.

```jsx
slickgrid.onSort.subscribe((e, args) => { // args: 정렬 정보.
	const { field } = args.sortCol;
	
	rows.sort((a, b) => {
		const result = 
			a[field] > b[field] ? 1 :
			a[field] < b[field] ? -1 :
			0;
			
		return args.sortAsc ? result : -result;
	});
	
	slickgrid.invalidate();			
});
```
