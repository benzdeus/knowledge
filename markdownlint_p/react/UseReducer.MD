# useReducer

เป็นการจัดการ State ในรูปแบบของ Redux โดยทั่วไป State สามารถอ่านค่าได้อย่างเดียวถ้าเราต้องการอยากจะเปลี่ยนค่า State จะใช้ useRedux โดยการกำหนดรูปแบบการกระทำที่เกิดขึ้นกับ State ของเราจะผ่านส่วนที่เรียกว่า Action มีค่าผลลัพธ์ 2 ตัว ผลลัพธ์จากการเปลี่ยนแปลง State และ Dispath(type,payload=body ที่ส่งไป) ส่วนการเรียกใช้ action ใน Reduce

การทำงาน เราต้อง import useReducer มาทุกครั้ง

```js
import React, { useReducer } from "react";
```

เรียกใช้ useReducer

```js
const [count, setCount] = useState(0);
const reducer = (state, action) => {
  switch (action.type) {
    case "ADD":
      return state + action.payload;
    case "SUB":
      return state - action.payload;
    case "CLEAR":
      return 0;
  }
};
const [result, dispatch] = useReducer(reducer, count);
```

นำผลลัพธ์จาก state ที่เกิดจากเปลี่ยนแปลงการ useReducer แสดง

```js
<div align="center" className="container">
  <h1>{result}</h1>
  <button onClick={() => dispatch({ type: "ADD", payload: 10 })}>เพิ่ม</button>
  <button onClick={() => dispatch({ type: "SUB", payload: 5 })}>ลบ</button>
  <button onClick={() => dispatch({ type: "CLEAR" })}>ล้าง</button>
</div>
```
