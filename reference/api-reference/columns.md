# Columns

#### grid.**autosizeColumns**()

셀의 내용과 상관없이 사용 가능한 수평 공간을 채우도록 모든열의 크기를 비례적으로 조정합니다.

#### grid.**getColumnIndex**(_id_)

> id - 열 아이디

지정된 id를 가진 열의 인덱스를 반환합니다. 사용자가 열을 다시 정렬할 수 있으므로 순서와 관계없이 열 정의를 가져오는데 사용할 수 있습니다.

```javascript
const column = grid.getColumns()[grid.getColumnIndex("title")]
```

#### grid.**getColumns**()

각 개별 컬럼에 대한 옵션 설정을 포함하는 열 정의 배열을 반환합니다.

```javascript
// 첫 번째 열을 정렬할 수 있는지 여부를 확인하기 위한 console.log
const cols = grid.getColumns();
const sortable = cols[0].sortable;
sortable ? console.log("It's sortable!") : console.log("It's not sortable!");
```

#### grid.**setColumns**(_columnDefinitions_)

> columnDefinitions - 열 정의 배열.

그리드 열을 설정합니다. 열 헤더가 다시 생성되고 렌더링 된 모든 행이 제거됩니다. 그리드를 다시 렌더링하려면`render()` 를 호출합니다.

```javascript
// 첫 번째 열의 이름은 First로 변경합니다.
const data = grid.getColumns();
data[0].name = "First";
grid.setColumns(data);
```

#### grid.**setSortColumn**(_columnId, ascending_)

`columId`(stiring)와 ascending(boolean)을 매개변수로 받습니다. 열의 헤더에 오름차순 또는 내림차순 형식의 정렬 글리프를 적용합니다. 열이 실제로 정렬되지는 않고 헤더에만 추가합니다.

#### grid.**setSortColumns**(_cols_)

다음과 같은 형태의 객체 배열을 매개변수로 받습니다.  `[ { columnId: [string], sortAsc: [boolean] }, ... ]`. 호출되면 배열의 지정된 각 열의 헤더에 오룸차순 또는 내림차순으로 정렬 글리프가 적용됩니다. 열이 실제로 정렬되지는 않고 헤더에만 추가합니다.

#### grid.**updateColumnHeader**(_columnId, title, toolTip_)

> `id` - 열 아이디
>
> `title` - 열의 새로운 이름
>
> `toolTip` - 열의 새로운 툴팁

기존 열 정의와 해당 헤더 DOM 요소를 새 제목 및 툴팁으로 업데이트 합니다.

```javascript
// 아이디가 "FirstName"인 열을 툴팁이 없는 "A First Name" 이름으로 변경합니다.
grid.updateColumnHeader("FirstName", "A First Name");
```
