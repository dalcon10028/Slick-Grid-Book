# Cells

#### grid.**addCellCssStyles**(_key, hash_)

> key - `setCellCssStyles`와 `removeCellCssStyles`를 호출하는데 사용할 수 있는 유일한 키 입니다. hash - 행 번호와 열 ID로 지정되는 추가 셀 CSS 클래스의 hash값 입니다.

예시:

```javascript
{ 
    0: { "number_column": "cell-bold", "title_column": "cell-title cell-highlighted" }, 
    4: { "percent_column": "cell-highlighted" } 
}
```

CSS 클래스에 "overlay"를 셀 DOM element에 추가합니다. SlickGrid는 서로 다른 키와 관련된 많은 오버레이를 가질 수 있으며 플러그인에 의해 종종 사용됩니다.

예를 들어, SlickGrid는 내부적으로 이 방법을 사용하여 선택한 셀을 SelectedCssClass로 장식합니다. (옵션 참조)

#### grid.**canCellBeActive**(_row, col_)

> `row` - 행 인덱스.
>
> `col` - 열 인덱스.

지정된 셀을 클릭하여 활성 포커스로 만들 수 있는 경우 `true`를 반환합니다.

#### grid.**canCellBeSelected**(_row, col_)

> `row` - 행 인덱스.
>
> `col` - 열 인덱스.

특정 셀을 선택했을 때 CellCssClass가 적용되면 `true`를 반환합니다. 셀이 존재하는데 비어 있는 경우에 셀을 선택할 수 있습니다.

#### grid.**editActiveCell**(_editor_)

> editor - slickgrid 에디터 (see examples in slick.editors.js).

활성 셀을 편집 모드로 전환하려고 시도합니다. 셀이 편집 불가능으로 설정된 경우 오류를 발생시킵니다.

지정된 `editor`를 사용합니다. 그렇지 않으면 지정된 셀에 대한 기본 편집기가 기본값으로 설정됩니다.

```javascript
// slickeditor.js가 포함된다고 가정하면...
// 첫 번째 행의 첫 번째 셀을 활성으로 설정합니다.

// 해당 셀에서 날짜 편집기를 호출.
grid.editActiveCell(Slick.Editors.Date);
```

#### grid.**flashCell**(_row, cell, speed_)

> `row` - 행 인덱스.
>
> `cell` - 열 인덱스.
>
> `speed` (선택사항) - 토글 호출 간의 지연 시간(밀리초)입니다. 기본값은 100ms입니다.

CSS 클래스를 4번 토글하여 셀을 두 번 깜빡입니다.

#### grid.**getActiveCell**()

현재 활성 셀의 좌표를 나타내는 개체를 반환합니다.

```javascript
{
  row: activeRow, 
  cell: activeCell
}
```

#### grid.**getActiveCellNode**()

현재 활성 셀을 포함하는 DOM 요소를 반환합니다. 활성화된 셀이 없으면 `null`이 반환됩니다.

```javascript
// 활성 셀에 대한 요소를 가져옵니다.
const $active = $(grid.getActiveCellNode())

// 활성 셀에 새 클래스 추가
$active.addClass('myClass');
```

#### grid.**getActiveCellPosition**()

활성 셀 위치에 대한 정보를 나타내는 개체를 반환합니다.

모든 좌표는 절대적이며 모든 조상의 가시성과 스크롤 위치를 고려합니다.

반환되는 객체는 다음과 같은 형태입니다.

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

#### grid.**getCellCssStyles**(_key_)

> key - 문자열

키를 받아 해당 이름으로 정의된 CSS 스타일 그룹을 반환합니다. 자세한 내용은 `[setCellCssStyles](<https://github.com/6pac/SlickGrid/wiki/Slick.Grid#wiki-setCellCssStyles>)`를 참조하십시오.

#### grid.**getCellEditor**()

활성중인 셀 편집기를 반환합니다. 현재 편집중인 셀이 없으면 `null`이 반환됩니다.

#### grid.**getCellFromEvent**(_e_)

> e - 표준 W3C/jQuery 이벤트.

표준 W3C/jQuery 이벤트에서 행 및 셀 인덱스를 포함하는 해시를 반환합니다.

Returns a hash containing row and cell indexes from a standard W3C/jQuery event.

#### grid.**getCellFromPoint**(_x, y_)

> `x` - x 좌표.
>
> `y` - y 좌표.

행 및 셀 인덱스를 포함하는 해시를 반환합니다. 좌표는 첫 번째 행(열 헤더 제외)으로 시작하는 그리드의 왼쪽 상단 모서리에 상대적입니다.

#### grid.**getCellNode**(_row, cell_)

> `row` - 행 인덱스.
>
> `cell` - 열 인덱스.

지정된 행 및 셀에 셀이 포함된 DOM element를 반환합니다.

#### grid.**getCellNodeBox**(_row, cell_)

> `row` - 행 인덱스.
>
> `cell` - 열 인덱스.

셀 위치에 대한 정보를 나타내는 객체를 반환합니다. 모든 좌표는 절대적이며 모든 조상 element들의 가시성과 스크롤 위치를 고려합니다.

객체는 다음과 같은 형태입니다:

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

#### grid.**gotoCell**(_row, cell, forceEdit_)

`row`(integer)과 `cell`(integer)를 받아, 행 인덱스와 셀 인덱스를 통해 보이도록 스크롤 합니다. 선택적으로 `forceEdit`(boolean)를 받아 참일 경우 지정된 셀 필드에 대한 편집을 시작합니다.

#### grid.**navigateDown**()

선택 불가능한 셀을 건너뛰고 활성 셀을 한 행 아래로 전환합니다. 수행을 완료 했는지 여부를 나타내는 `boolean`을 반환합니다.

#### grid.**navigateLeft**()

선택 불가능한 셀을 건너뛰고 활성 셀을 한 열 왼쪽으로 전환합니다. 첫 번째 셀에서 `navigatePrev`, `navigateLeft`은 이동하지 않고 멈춥니다. 수행을 완료 했는지 여부를 나타내는 `boolean`을 반환합니다.

#### grid.**navigateNext**()

활성 셀 위에 있는 다음 선택이 가능한 셀을 탭합니다. 수행을 완료 했는지 여부를 나타내는 `boolean`을 반환합니다.

#### grid.**navigatePrev**()

활성 셀을 이전 선택 가능한 셀로 탭합니다. 수행을 완료 했는지 여부를 나타내는 `boolean`을 반환합니다.

#### grid.**navigateRight**()

선택 불가능한 셀을 건너뛰고 활성 셀 하나를 오른쪽으로 전환합니다. 마지막 셀에서 `navigateNext`, `navigateRight`은 이동하지 않고 멈춥니다. 수행을 완료 했는지 여부를 나타내는 `boolean`을 반환합니다.

#### grid.**navigateUp**()

선택 불가능한 셀을 건너뛰고 활성 셀을 한 행 위로 전환합니다. 수행을 완료 했는지 여부를 나타내는 `boolean`을 반환합니다.

#### grid.**removeCellCssStyles**(_key_)

> key - 문자열.

셀 DOM 요소에서 CSS 클래스의 `overlay`를 제거합니다. 자세한 내용은 `[setCellCssStyles](<https://github.com/6pac/SlickGrid/wiki/Slick.Grid#wiki-setCellCssStyles>)`를 참조하십시오.

#### grid.**resetActiveCell**()

활성중인 셀을 재설정합니다.

#### grid.**setActiveCell**(_row, cell_)

> `row` - 행 인덱스.
>
> `cell` - 열 인덱스.

활성 셀을 설정합니다.

#### grid.**setCellCssStyles**(_key, hash_)

> `key` - 문자열. 키와 이미 연결된 모든 데이터를 덮어씁니다.
>
> `hash` - 행 번호 및 열 id로 지정되는 추가적인 셀 CSS 클래스의 해시입니다. 여러 CSS 클래스를 지정하고 공백으로 구분할 수 있습니다.
>
> 예시:
>
> ```jsx
> { 
>     0: { 
>         "number_column": "cell-bold", 
>         "title_column": 
>         "cell-title cell-highlighted" 
>         }, 
>     4: { "percent_column": "cell-highlighted" } 
> }
> ```

`removeCellCssStyles(key)`다음에 `addCellCssStyles(key, hash)`를 호출하여 CSS 클래스를 특정 그리드 셀로 설정합니다. 키는 이 스타일 집합의 이름이므로 나중에 이를 수정하거나 제거할 수 있습니다. 예를 들어, 해시는 적용할 CSS 클래스의 행 인덱스, 열이름이 중첩된 해시입니다.

다음과 같은 열이 있는 grid가 있다고 가정합니다:

```javascript
["login", "name", "birthday", "age", "likes_icecream", "favorite_cake"]
```

그리고 오늘 생일인 사람의 "birthday", "age"열을 강조 표시합니다. 이 경우엔 0과 9 인덱스 입니다. (그리드의 첫 번째 행과 10번째 행).

```css
.highlight{ background: yellow }
```

```javascript
grid.setCellCssStyles("birthday_highlight", {
   0: {
        birthday: "highlight", 
        age: "highlight" 
       },
   9: {
         birthday: "highlight",
         age: "highlight"
       }
})
```
