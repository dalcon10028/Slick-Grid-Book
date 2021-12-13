# Core

#### grid.init()

그리드 초기화 합니다. 플러그인들이 등록된 후 호출됩니다. 보통 `constructor`에서 호출하므로 따로 호출하지 않아도 됩니다. 그러나 특정 경우에 다른 프로세스가 완료될 때까지 초기화를 연기해야 할 수도 있습니다. 이 경우 `explicitInitialization` 옵션을 `true`로 설정하고 `grid.init()`을 수동으로 호출합니다.

#### grid.getData()

`DataView` 객체를 사용하는 경우 `DataView` 객체를 반환하고, 아닐경우 모든 데이터 객체의 배열을 반환합니다.

#### grid.getDataItem(index)

> index - .아이템 인덱스

인덱스에 해당하는 아이템을 반환합니다.

```jsx
// Get the id of the 15th item
var id15 = grid.getDataItem(14).id;
```

#### grid.**setData**(_newData, scrollToTop_)

> data - 새로운 데이터 바인딩 소스. 일반적인 javascript 배열이거나 getItem(index)와 getLength() 함수를 노출하는 사용자 지정 객체일 수 있습니다.

> scrollToTop - `true`일 경우에 그리드의 스크롤 위치를 상단으로 재설정 합니다.

데이터 바인딩을 위해 새 소스를 설정하고 렌더링된 모든 행을 제거합니다. 이렇게 하면 새 행이 렌더링되지 않습니다. `render()` 호출을 통해 새 행을 렌더링할 수 있습니다.

#### grid.**getDataLength**()

데이터 바인딩 소스의 크기를 반환합니다.

```jsx
// 모든 데이터 목록에서 아이디만 추출해 배열 생성
const ids = [];
for (let i=0; i < grid.getDataLength(); i++) {
  ids.push(grid.getDataItem(i).id);
}
```

#### grid.**getOptions**()

그리드에 설정된 모든 옵션을 포함하는 객체를 반환합니다. [그리드 옵션 목록보기](https://github.com/6pac/SlickGrid/wiki/Grid-Options)

```jsx
// 현재 선택된 모든 요소 찾기
const $selectedCells = $('.' + grid.getOptions().selectedCellCssClass);
```

#### grid.**getSelectedRows**()

현재 선택한 행에 해당하는 행 인덱스 배열을 반환합니다.

#### grid.**getSelectionModel**()

현재 [SelectionModel](https://github.com/6pac/SlickGrid/wiki/Handling-selection)을 반환합니다.

#### grid.**setOptions**(_options_)

> options - 구성 옵션이 있는 객체.

지정된 해시를 사용하여 그리드 옵션을 확장합니다. 편집중인 셀이 있는 경우, 그리드는 변경 사항을 커밋하려고 시도하고 성공할 경우에만 계속합니다.

```jsx
// 선택한 셀에 대해 새 CSS 클래스 설정
grid.setOptions( { selectedCellCssClass: "newSelection" } );

// 첫 번째 행 선택
grid.setSelectedRows([0]);

// 선택한 셀의 element들을 가져옵니다.
$('.newSelection');
```

#### grid.**setSelectedRows**(_rowsArray_)

> rowsArray - 행 번호 배열

행의 인덱스 배열을 매개변수로 받아 `selectable`플래그 여부에 따라 현재 선택된 `selectedCellCssClass`를 셀에 적용합니다.

```jsx
// 처음 세 줄을 선택
grid.setSelectedRows([0, 1, 2]);
```

#### grid.**setSelectionModel**([_selectionModel_](https://github.com/6pac/SlickGrid/wiki/Handling-selection))

현재 [selectionModel](https://github.com/6pac/SlickGrid/wiki/Handling-selection)의 등록을 취소하고 새 모델을 등록합니다.
