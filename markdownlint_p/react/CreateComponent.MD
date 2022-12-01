# การสร้าง Component

#### Components ทำให้สามารถแบ่ง UI ที่มีความซับซ้อนออกเป็นส่วนเล็กๆที่ทำงานได้อย่างอิสระ และสามารถนำไปใช้ซ้ำได้ ใน React สามารถสร้าง Components ได้แบบ function และ class ซึ่งขึ้นอยู่กับการนำไปใช้งาน แต่ทั้งคู่จะ return ออกมาเป็นเหมือน HTML element ทั่วๆไป

- ในที่นี้จะขอยกตัวอย่างการสร้าง Component ประเภท Class Component และ Function Component

- การสร้าง Component แบบ Class Component
  
```js
class Example extends React.Component {
  render() {
    return <h2>Hi, I am Example!</h2>;
  }
}
export default Example
```
  - การสร้าง Component แบบ Function Component คนส่วนใหญ่จะนิยมเขียนแบบ  Function Component เพราะไม่มีการประกาศ render() แบบ Class Component แต่จะสามารถ return() ค่าออกมาได้เลย 
  
```js
// Example1
export default function Example() {
     return (
        <h2>Hi, I am Example!</h2>
     )
}
```

```js
// Example2
function Example() {
    return (
        <h2>Hi, I am Example!</h2>
     )
}
export default Example;
```
```js
// Example3
const Example = () =>{
    return (
        <h2>Hi, I am Example!</h2>
     )
}
export default Example;
```





