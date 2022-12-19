# การใช้งาน useRef createRef และ forwardRef

## useRef

คือ React Hooks ที่สามารถเข้าถึงโดยการ Reference ไปที่ DOM element ใช้กับ Functional component สามารถทำ initialValue (.current) ได้

## คุณสมบัติของ useRef

- ใช้กับ Functional component
- สามารถกำหนด initialValue (.current) ได้
- เพื่อรักษาค่า Ref ปัจจุบันใช้อยู่ตลอดการใช้งานของ Functional component และเมื่อมีการ Re-Render จะไม่สร้างค่า Ref ขึ้นมาใหม่
- ความสามารถในการทำ Memorize
- อัปเดตค่า .current ได้ (แต่ต้องสั่ง Trigger อะไรบางอย่างให้ Re-Render จากนั้นค่าที่กำหนดถึงจะเปลี่ยนแปลง)

```js
// Step1: import useRef from react
import React, { useRef, useEffect } from "react";

const RefCase1 = () => {
  // Step2: ประกาศตัวแปร useRef
  const titleRef = useRef();

  useEffect(function () {
    setTimeout(() => {
      // Step4: update ค่าผ่าน current attribute
      titleRef.current.textContent = "Updated Text";
    }, 2000);
  }, []);

  return (
    <>
      // Step3: ผูกตัวแปรจาก Step2 กับ element ใน jsx
      <div ref={titleRef}>Original title</div>
    </>
  );
};

export default RefCase1;
```

## createRef

คือ วิธีการ Access DOM nodes ด้วยการ Reference ใช้กับ Class component (การทำงานคล้ายกับ useRef)

## คุณสมบัติของ useRef

- ใช้กับ Class component
- เมื่อต้องการรีเช็ต Ref ใหม่ทุกครั้งที่มีการ Re-Render

```js
import { Component, createRef } from "react";

export default class Form extends Component {
  inputRef = createRef();

  handleClick = () => {
    this.inputRef.current.focus();
  };

  render() {
    return (
      <>
        <input ref={this.inputRef} />
        <button onClick={this.handleClick}>Focus the input</button>
      </>
    );
  }
}
```

## forwardRef

คือ การส่งต่อ Ref จาก Parent ไปที่ Child เมื่อสร้างเป็น Ref เป็น Component

```js
import React, {useRef, forwardRef} from 'react';
export function ParentComponent() {
 const nodeRef = useRef(null); return (
    <ChildComponent ref={nodeRef}
    )};

export function ChildComponent forwardRef((props, ref) {
 return (
     <div ref={ref}>
        <p>Pass refs like this</p>
     </div>
 )
});
```
