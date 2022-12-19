# useContext

Hook API ที่ช่วยในการจัดการกับ global state คล้าย ๆ กับ redux ซึ่งหลักการของเจ้าตัว Context Api มันจะเป็นการไปบอก component ที่ชั้น parent หรือ top level component ว่าจะให้ค่า context เป็นอย่างไร แล้ว component ลูกที่อยู่ใต้มันจะสามารถนำค่า context ไปใช้ได้

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
