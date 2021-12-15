# Rendering

#### grid.**getCanvasNode**()

DOM에서 현재 렌더링 중인 모든 데이터 행을 포함하는 `grid-canvas`클래스에 일치하는 DIV element를 반환합니다.

```javascript
// DOM에서 렌더링 되는 총 데이터 행 수를 가져옵니다.
const numRenderedRows = $(grid.getCanvasNode()).children().length;
```

#### grid.**getGridPosition**()

페이지에서 그리드 위치에 대한 정보를 나타내는 객체를 반환합니다.

객체는 다음과 같은 형태를 취합니다:

```javascript
{ 
    bottom:  [numPixels],
    height:  [numPixels],
    left:    [numPixels], 
    right:   [numPixels], 
    top:     [numPixels], 
    visible: [boolean], 
    width:   [numPixels] 
}
```

#### grid.**getRenderedRange**(_viewportTop, viewportLeft_)

> `viewportTop` (optional) - 그리드의 맨 위에서 offset되는 픽셀 수 입니다.
>
> `viewportLeft` (optional) - 그리드의 맨 왼쪽에서 offset되는 픽셀 수 입니다.

매개변수를 전달하지 않으면, 현재 렌더링 중인 행의 범위(행 번호)와 현재 렌더링된 픽셀의 왼쪽/오른쪽 범위를 알려주는 개체를 반환합니다.

```javascript
{ 
    top: [rowIndex], 
    bottom: [rowIndex], 
    leftPx: [numPixels], 
    rightPx: [numPixels] 
}
```

`viewportTop`와 `viewportLeft`는 선택사항이며, 특정 스크롤 상단/왼쪽 간격띄우기에서 렌더링할 항목을 지정합니다. 예를 들어 `grid.getRenderedRange(1000)`는 다음과 같이 질문한다: "만약 1000픽셀을 아래로 스크롤한다면, 어떤 행이 렌더링될 것인가?"

#### grid.**getViewport**(_viewportTop, viewportLeft_)

> `viewportTop` (optional) - 그리드의 맨 위에서 offset되는 픽셀 수 입니다.
>
> `viewportLeft` (optional) - 그리드의 맨 왼쪽에서 offset되는 픽셀 수 입니다.

현재 화면에 표시되는 행과 왼쪽/오른쪽 스크롤을 위한 픽셀 오프셋을 알려주는 객체를 반환합니다.

```javascript
{ 
    top: [rowIndex], 
    bottom: [rowIndex], 
    leftPx: [numPixels], 
    rightPx: [numPixels] 
}
```

또한 `viewportTop`와 `viewportLeft` 오프셋을 허용하여 해당 지점까지 스크롤할 경우 사용자에게 표시되는 내용을 알려줍니다.

#### grid.**invalidate**()

그리드를 다시 그립니다. 모든 행 및 `render()`호출을 무효화합니다.

```javascript
// 첫 번째 행의 이름 name 속성 변경
const data = grid.getData();
data[0].name = "New name!"

// 데이터를 다시 렌더링하기 위해 invalidate 호출. render()를 호출할 필요 없습니다.
grid.invalidate();
```

#### grid.**invalidateAllRows**()

테이블의 모든 행이 유효하지 않음을 그리드에 알립니다. (이후에 `render()`가 호출되면 전체 그리드를 다시 그립니다.)

#### grid.**invalidateRow**(_row_)

> row - 행 인덱스.

`row`로 지정된 행이 잘못되었음을 그리드에 알립니다. (이후에 `render()`가 호출되면 전체 그리드를 다시 그립니다.)

#### grid.**invalidateRows**(_rows_)

> rows - 행 인덱스 배열.

행 인덱스 배열을 받아 해당 행이 유효하지 않음을 그리드에 알립니다. (이후에 `render()`가 호출되면 해당 행의 내용을 다시 그립니다.)

```javascript
// 첫 번째 행의 이름 속성 변경
const data = grid.getData();
data[0].name = "New name!"
data[1].name = "Another new name!"

// 처음 두 행을 무효화 하려면 invalidateRows를 호출합니다.
grid.invalidateRows([0,1]);

// 처음 두 행을 다시 렌더링합니다.
grid.render();
```

#### grid.**render**()

DOM에 SlickGrid를 렌더링 합니다.

#### grid.**resizeCanvas**()

현재 DIV 컨테이너에 맞게 캔버스 크기를 조정합니다. (예를 들어, 그리드 크기를 조정하기 위해 먼저 div의 크기를 변경한 다음 `resizeCanvas()`를 호출합니다.

#### grid.**scrollCellIntoView**(_row, cell_)

> `row` - 행 인덱스.
>
> `cell` - 열 인덱스.

표시된 셀 보기로 스크롤 합니다.

표시된 열이 이미 보기에 없는 경우 이 작업은 아무것도 수행하지 않습니다. 예를 들어, 그리드가 맨 왼쪽으로 스크롤 된 상태로 0행에서 `scrollCellIntoView(100,0)`를 호출해도 단순히 100행으로 스크롤되지 않습니다. 그러나 8열이 보이지 않을 때, `scrollCellIntoView(100,8)`를 호출하면 아래로 스크롤하여 오른쪽으로 스크롤 합니다.

#### grid.**scrollRowIntoView**(_row, doPaging_)

> row - 행 인덱스.
>
> `doPaging` - boolean 값. 만약 `false`면 표시된 행이 view의 맨 위에 오도록 그리드가 스크롤됩니다. True이면 그리드가 스크롤 되어 표시된 행이 보기의 맨 아래에 오도록 합니다. 기본값은 `false`입니다.

표시된 행까지 view를 스크롤합니다.

#### grid.**scrollRowToTop**(_row_)

> row - 행 인덱스.

표시된 행으로 view를 스크롤 하여 행을 view의 맨 위에 배치합니다.

#### grid.**updateCell**(_row, cell_)

TODO

```jsx
// put stuff here
```

#### grid.**updateRow**(_row_)

TODO

```jsx
// put stuff here
```

#### grid.**updateRowCount**()

TODO

```jsx
// put stuff here
```
