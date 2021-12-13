# Constructor

```javascript
const grid = new Slick.Grid(*container, data, columns, options*);
```

> `container` - 그리드안에 컨테이너 노드를 생성합니다. DOM Element가 될 수 있고, jQuery node가 될 수 있고 jQuery selector가 될 수 있습니다. `data` - 데이터 바인딩 소스. 일반적인 javascript 배열이거나 getItem(index)와 getLength() 함수를 노출하는 사용자 지정 객체일 수 있습니다. `columns` - 컬럼 정의 객체의 배열. 각 컬럼 정의 객체에 포함할 수 있는 옵션 목록은 [Column Options](https://github.com/6pac/SlickGrid/wiki/Column-Options)를 참고합니다. `options` - 추가 옵션. 추가 옵션 목록은 [Grid Options](https://github.com/6pac/SlickGrid/wiki/Grid-Options)를 참고합니다.

그리드 인스턴스 생성.

[사용예제](https://mleibman.github.io/SlickGrid/examples/example1-simple.html)를 확인할 수 있습니다.

```javascript
let grid;
const columns = [
  {id: "title", name: "Title", field: "title"},
  {id: "duration", name: "Duration", field: "duration"},
  {id: "%", name: "% Complete", field: "percentComplete"},
  {id: "start", name: "Start", field: "start"},
  {id: "finish", name: "Finish", field: "finish"},
  {id: "effort-driven", name: "Effort Driven", field: "effortDriven"}
];

const options = {
  enableCellNavigation: true,
  enableColumnReorder: false
};

$(() => {
	const data = [];
	for (var i = 0; i < 500; i++) {
		data.push({
	    title: "Task " + i,
	    duration: "5 days",
	    percentComplete: Math.round(Math.random() * 100),
	    start: "01/01/2009",
	    finish: "01/05/2009",
	    effortDriven: (i % 5 == 0)
	});
}

grid = new Slick.Grid("#myGrid", data, columns, options);
```
