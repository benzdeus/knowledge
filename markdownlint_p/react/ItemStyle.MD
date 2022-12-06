# Item Style

คือการจำหนด Style ให้กับ component รวมไปถึงรูปแบบข้อมูล และการแสดงผล

```js
import React from "react";
import propTypes from "prop-types";
import "./custom.css";

Item.propTypes = {
  title: propTypes.string.isRequired,
  amount: propTypes.number.isRequired,
};
export default function Item(props) {
  const { title, amount } = props;

  //   ประกาศตัวแปรเพื่อกำหนด style
  const states = amount < 0 ? "expense" : "income";

  //    ประกาศตัวแปรเพื่อกำหนดการแสดงผล
  const symbol = amount < 0 ? "-" : "+";

  return (
    <li className={states}>
      <div className="row">
        <div className="col-8">{title}</div>
        <div className="col-4 text-right">
          {symbol}
          {Math.abs(amount)}
        </div>
      </div>
    </li>
  );
}
```

- import class css ที่ไฟล์ ./custom.css เพื่อใช้ style การแสดงผล

```css
.expense {
  border-right: 5px solid red;
  color: red;
}
.income {
  border-right: 5px solid #2ccc71;
  color: #2ccc71;
}
```
