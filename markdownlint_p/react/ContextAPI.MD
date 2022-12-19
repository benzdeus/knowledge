# Context API (Global State)

ข้อมูลที่สามารถเข้าถึงได้ในทุกส่วนของ Component ความหมายคือ สามารถเข้าถึงข้อมูลชุดเดียวกันได้โดยที่ไม่ต้องใช้รูปแบบส่งข้อมูลจาก component แม่ไปยัง component ลูก มีองค์ประกอบ 2 แบบ

- Provider(Parent) ดูแลและจัดการข้อมูลแล้วนำไปส่งให้ Cunsumer
- Consumer(Children) นำข้อมูลที่ได้จาก Provider ไปสร้างหรือแสดงผลใน component

## วิธีการนำข้อมูลใน Context API (Global State) ไปใช้งานใน Component สามารถเขียนได้ 2 วิธี

## DataContext

- สร้างไฟล์หนึ่งขึ้นมา ในที่นี้จะสร้างไฟล์ DataContext เวลานำไปใช้ใน component ต้อง import ไฟล์ DataContext ทุกครั้ง และกำหนดสถานะ Consumer

ต้อง import DataContext เสมอถึงจะสามารถใช้ DataContext

```js
import DataContext from "../data/DataContext";
```

ตัวอย่างการทำงาน

สร้างไฟล์ DataContext ให้เป็น Provider

```js
import { createContext } from "react";

const DataContext = createContext();

export default DataContext;
```

ไฟล์แม่ main ที่ส่งข้อมูลมาให้ลูก

```js
import React from "react";
import DataContext from "../data/DataContext";
import FormComponent from "./FormComponent";
import Transaction from "./Transaction";

export default function Main() {
  return (
    <DataContext.Provider value={"Pang_Babi"}>
      <div className="container">
        <h1 style={design}>แอพบัญชีรายรับ-รายจ่าย</h1>
        <FormComponent onAddItem={onAddNewItem} />
        <Transaction items={items} />
      </div>
    </DataContext.Provider>
  );
}
```

ไฟล์ลูกที่รับค่ามาจากแม่โดยใช้ useContext

```js
import React from "react";
import DataContext from "../data/DataContext";

export default function Children() {
  return (
    <div>
      <DataContext.Consumer>{(value) => <p>{value}</p>}</DataContext.Consumer>
    </div>
  );
}
```

## useContext

- useContext ให้ import useContext และประกาศตัวแปรรับค่าใน useContext และสามารถนำค่าไปแสดงได้เลย

ต้อง import useContext เสมอถึงจะสามารถใช้ useContext

```js
import React, { useContext } from "react";
```

การใช้งานประการตัวแปรรับเพื่อรับค่าที่ส่งมา

```js
const { name } = useContext(DataContext);
```

ตัวอย่างการทำงาน

สร้างไฟล์ DataContext ให้เป็น Provider

```js
import { createContext } from "react";

const DataContext = createContext();

export default DataContext;
```

ไฟล์แม่ main ที่ส่งข้อมูลมาให้ลูก

```js
import React from "react";
import DataContext from "../data/DataContext";
import FormComponent from "./FormComponent";
import Transaction from "./Transaction";

export default function Main() {
  return (
    <DataContext.Provider value={"Pang_Babi"}>
      <div className="container">
        <h1 style={design}>แอพบัญชีรายรับ-รายจ่าย</h1>
        <FormComponent onAddItem={onAddNewItem} />
        <Transaction items={items} />
      </div>
    </DataContext.Provider>
  );
}
```

ไฟล์ลูกที่รับค่ามาจากแม่โดยใช้ useContext

```js
import React, { useContext } from "react";

export default function Children() {
  const { name } = useContext(DataContext);
  return <div>{name}</div>;
}
```

## Context API (Multiple Value) การส่งข้อมูลไปได้หลายค่า อย่างเช่น ก้อนช้อมูลแบบ object

- ไฟล์แม่

  ```js
  import React, { useState, useEffect } from "react";
  function App() {
    const [reportIncome, setReportIncome] = useState(0);
    const [reportExpense, setReportExpense] = useState(0);

    useEffect(() => {
      const amounts = items.map((items) => items.amount);
      const income = amounts
        .filter((elemnet) => elemnet > 0)
        .reduce((total, elemnet) => (total += elemnet), 0);
      const expense =
        amounts
          .filter((elemnet) => elemnet < 0)
          .reduce((total, elemnet) => (total += elemnet), 0) * -1;
      setReportIncome(income);
      setReportExpense(expense);
    }, [items]);

    return (<div>
        <DataContext.Provider value={"Pang_Babi"}>
          <div className="container">
            <h1 style={design}>แอพบัญชีรายรับ-รายจ่าย</h1>
            <FormComponent onAddItem={onAddNewItem} />
            <Transaction items={items} />
          </div>
        </DataContext.Provider>
      </div>
    );
  }
  export default App;
  ```

  - ไฟล์ลูก useContext

```js
import React, { useContext } from "react";
import "./custom.css";

export default function ReportComponent() {
  const { income, expense } = useContext(DataContext);

  const formatNumber = (num) => {
    return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
  };
  return (
    <div className="pt-3">
      <h6>ยอดคงเหลือ (บาท) </h6>
      <h1>฿{formatNumber((income - expense).toFixed(2))}</h1>
      <div className="report-container">
        <div>
          <h6>รายได้ทั้งหมด</h6>
          <p className="report plus">฿{formatNumber(income)}</p>
        </div>
        <div>
          <h6>รายจ่ายทั้งหมด</h6>
          <p className="report minus">฿{formatNumber(expense)}</p>
        </div>
      </div>
    </div>
  );
}
```

- ไฟล์ลูก DataContext

```js
import React from "react";
import DataContext from "../data/DataContext";
import "./custom.css";

export default function ReportComponent() {
  const formatNumber = (num) => {
    return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
  };
  return (
    <div>
      <DataContext.Consumer>
        {(value) => (
          <p>
            รายจ่าย: {value.income} รายจ่าย: {value.expense}{" "}
          </p>
        )}
      </DataContext.Consumer>
    </div>
  );
}
```
