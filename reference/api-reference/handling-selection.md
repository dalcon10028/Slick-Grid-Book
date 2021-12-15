# Handling selection

SlickGrid에서 셀 선택은 `selection model`에서 처리 됩니다.

**selection model**은 사용자와의 상호작용을 처리하고 subscribers에게 선택 사항의 변경 사항을 알리는 역할을 하는 컨트롤러 입니다. Selection은 Slick.Range 객체의 배열로 표현됩니다.



`getSelectionModel()`을 호출하여 그리드에서 현재 selection model을 가져오고 `setSelectionModel(selectionModel)`을 사용하여 다른 모델을 설정할 수 있습니다. 기본적으로 selection model은 설정되지 않습니다. 활성화 예제는 **Row Selection**을 참조하십시오.



그리드는 개발을 단순화 하는 두 가지 helper method인 `getSelectedRows()` 및 `setSelectedRows(rowsArray)`와 `onSelectedRowsChanged` 이벤트를 제공합니다.



SlickGrid에는 두 가지 사전 제작된 `Slick.CellSelectionModel`과 `Slick.RowSelectionModel`이 포함되어 있지만, 사용자 정의 모델을 쉽게 작성할 수 있습니다.



#### 초기화(init)

`function init(grid)`

`selection model`이 `setSelectionModel`로 등록될 때마다 그리드 인스턴스와 함께 호출되는 초기화 함수 입니다. `selection model`은 이를 사용하여 상태를 초기화하고 그리드 이벤트를 구독할 수 있습니다.

#### 소멸(destroy)

`function destroy()`

다른 `selection model`로 `setSelectionModel`을 호출하여 `selection model`이 그리드에서 등록 취소될 때, 또는 `selection model`을 가진 그리드가 소멸될 때 호출되는 함수 입니다. `selection model`은 이 함수를 사용하여 그리드 이벤트의 구독을 취소하고 모든 리소스(DOM 노드, 이벤트 리스너 등)을 해제할 수 있습니다.

#### 선택 영역 변경(**onSelectedRangesChanged)**

`Slick.Event`

선택 범위가 변결 될 때마다 발생하는 이벤트 입니다. selection model이 그리드에 등록되면 그리드는 이 이벤트를 등록해 내부 상태를 업데이트하고 선택할 셀을 SelectedCssClass로 장식하는 데 사용합니다. 이벤트는 다음과 같은 데이터로 이벤트 인자에서 발생해야 합니다.

```jsx
ranges - 선택 영역을 나타내는 Slick.Range 객체 입니다.
```

다음은 마우스 클릭에만 반응하는 단일 셀 selection model의 간단한 예입니다:

```jsx
class SingleCellSelectionModel {
	constructor(grid) {
		this.grid = grid;
		this.grid.onClick.subscribe(this.handleGridClick);
	}

	destroy() {
		this.grid.onClick.unsubscribe(this.handleGridClick);	
	}

	handleGridClick(e, args) {
		const cell = this.grid.getCellFromEvent(e);
		if (!cell || !this.grid.canCellBeSelected(cell.row, cell.cell)) {
			return;		
		}

		this.onSelectRangesChanged.notify([new Slick.Range(cell.row, cell.cell, cell.row, cell.cell)]);
	}
}
```

### Row Selection

include 된 row seletion plugin을 사용하도록 설정하려면 다음과 같이 합니다:

```html
/* In your html head */
<script src="path/to/SlickGrid/plugins/slick.rowselectionmodel.js"></script>

/* In your javascript file */
slickGrid.setSelectionModel(new Slick.RowSelectionModel());
slickGrid.init();

/* In your css file (or you can use a default theme that has this selector) */
.slick-cell.selected {
    background-color: #FBB;
}
```
